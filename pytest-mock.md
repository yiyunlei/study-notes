# Pytest unit test mock







```python
def patch(
        target, new=DEFAULT, spec=None, create=False,
        spec_set=None, autospec=None, new_callable=None, **kwargs
    ):
```

spec=True或spec_set=True用于将Mock对象设置为spec/spec_set对象



## Spec参数 (specification)

在`unittest.mock.patch`函数中，`spec`参数允许你为模拟对象设置一个规范(spec)，这个规范基于现有的对象。如果你设置了`spec`参数，那么模拟对象将会包含现有对象的所有方法和属性，并且如果你试图访问模拟对象上不存在于现有对象上的属性或方法，Python将会抛出`AttributeError`异常。这可以防止在测试中因为拼写错误或者其他错误而不小心创建并使用了不存在的方法或属性。

例如，如果你有一个类`Foo`如下：

```python
class Foo:
    def bar(self):
        return "bar"
```

你可以这样创建一个模拟对象：

```python
from unittest.mock import Mock
foo = Foo()
mock_foo = Mock(spec=foo)
```

然后你可以像正常调用`foo.bar`那样调用`mock_foo.bar`。但是如果你试图调用`mock_foo.baz`（`Foo`类中并没有`baz`方法），Python将会抛出`AttributeError`异常。

注意，虽然模拟对象包含了现有对象的所有方法和属性，但是这些方法和属性的行为是可以被你控制的。也就是说，你可以设定这些方法和属性在被调用时应该返回什么结果，或者应该抛出什么异常等等。

关于其他参数的简要解释：

- `target`：需要被替换的对象的路径，必须是一个字符串。
- `new`：模拟对象的类型，默认是`MagicMock`。
- `create`：如果为`True`，那么即使`target`指定的路径不存在，`patch`也会创建一个模拟对象。
- `spec_set`：和`spec`类似，但是如果设定了`spec_set`，那么试图设置模拟对象上不存在于现有对象上的属性将会抛出`AttributeError`异常。
- `autospec`：如果为`True`，那么`patch`将会自动创建一个和`target`指定的对象相同的规范。
- `new_callable`：用于创建模拟对象的可调用对象，默认是`MagicMock`。
- `**kwargs`：这些关键字参数将会被用来创建模拟对象。





## References

- [知乎 - Python 中 Mock 到底该怎么玩？一篇文章告诉你（超全)](https://zhuanlan.zhihu.com/p/345988487)

- [个人博客 - 单元测试mock模块介绍](https://hustyichi.github.io/2018/11/24/mock)