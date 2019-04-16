## 学习Django中ORM的实现
- 创建类的时候对min_value, max_value等进行检查, 在__init__中
- 对类赋值的时候对min_value, max_value等进行检查, 在__get__中
```
import numbers

class Field:
    pass

class IntField(Field):
    # 数据描述符
    def __init__(self, db_column, min_value=None, max_value=None):
        self._value = None
        self.min_value = min_value
        self.max_value = max_value
        self.db_column = db_column
        if min_value is not None:
            if not isinstance(min_value, numbers.Integral):
                raise ValueError("min_value must be int")
            elif min_value < 0:
                raise ValueError("min_value must be positive int")
        if max_value is not None:
            if not isinstance(max_value, numbers.Integral):
                raise ValueError("max_value must be int")
            elif max_value < 0:
                raise ValueError("max_value must be positive int")
        if min_value is not None and max_value is not None:
            if min_value > max_value:
                raise ValueError("min_value must be smaller than max_value")

    def __get__(self, instance, owner):
        return self._value

    def __set__(self, instance, value):
        if not isinstance(value, numbers.Integral):
            raise ValueError("int value need")
        if value < self.min_value or value > self.max_value:
            raise ValueError("value must between min_value and max_value")
        self._value = value


class CharField(Field):
    def __init__(self, db_column, max_length=None):
        self._value = None
        self.db_column = db_column
        if max_length is None:
            raise ValueError("you must spcify max_lenth for charfiled")
        self.max_length = max_length

    def __get__(self, instance, owner):
        return self._value

    def __set__(self, instance, value):
        if not isinstance(value, str):
            raise ValueError("string value need")
        if len(value) > self.max_length:
            raise ValueError("value len excess len of max_length")
        self._value = value


class ModelMetaClass(type):
    def __new__(cls, name, bases, attrs, **kwargs):
        # BaseModel类的创建也是通过该元类, 但是不需要执行下面的内容
        if name == "BaseModel":
            return super().__new__(cls, name, bases, attrs, **kwargs)
        # 在attrs中有传入的参数, Meta等, 需要进行处理
        fields = {}
        for key, value in attrs.items():
            if isinstance(value, Field):
                fields[key] = value
        attrs_meta = attrs.get("Meta", None)
        _meta = {}
        db_table = name.lower()
        if attrs_meta is not None:
            table = getattr(attrs_meta, "db_table", None)
            if table is not None:
                db_table = table
        _meta["db_table"] = db_table
        attrs["_meta"] = _meta
        attrs["fields"] = fields
        del attrs["Meta"]
        return super().__new__(cls, name, bases, attrs, **kwargs)


class BaseModel(metaclass=ModelMetaClass):
    # 在__new__中只是对参数进行处理, 并返回cls, 并没有赋给user对象
    def __init__(self, *args, **kwargs):
        for key, value in kwargs.items():
            setattr(self, key, value)
        return super().__init__()

    # 生成sql语句保存到数据库中
    def save(self):
        fields = []
        values = []
        for key, value in self.fields.items():
            db_column = value.db_column
            if db_column is None:
                db_column = key.lower()
            fields.append(db_column)
            value = getattr(self, key)
            values.append(str(value))

        sql = "insert {db_table}({fields}) value({values})".format(db_table=self._meta["db_table"],
                                                                   fields=",".join(fields), values=",".join(values))
        pass

class User(BaseModel):
    name = CharField(db_column="name", max_length=10)
    age = IntField(db_column="age", min_value=1, max_value=100)

    class Meta:
        db_table = "user"


if __name__ == "__main__":
    # user = User(name="bobby", age=28)
    user = User()
    user.name = "bobby"
    user.age = 28
    user.save()
```