# Init Net

## 1. AttributeError: '*' object has no attribute 'weight'

```python
AttributeError: 'CE_Decoder_Conv_Block' object has no attribute 'weight'
```

My class name is 'CE_Decoder_Conv_Block', and my init function is like this:

```python
def weights_init(m, init_type='normal', init_gain=0.02):
    """Initialize network weights."""
    classname = m.__class__.__name__
    if classname.find("Conv") != -1:
        nn.init.normal_(m.weight, 0.0, init_gain)
    elif classname.find("BatchNorm") != -1:
        nn.init.normal_(m.weight, 1.0, 0.02)
        nn.init.constant_(m.bias, 0.0)

    print('initialize network with %s' % init_type)
```

Because I use the method "find", it search "Conv" in classname as searching string. My class 'CE_Decoder_Conv_Block' is a sequence of some layers, the convolution layers in it have attribute "weight", however, the sequence block does not have attribute "weight".

### Solution One

Change class name to 'CE_Decoder_conv_Block', then the string search will not regard the sequence block as a single  convolution layer.

### Solution Two

Write the checks as this, especially when using torch.nn.Module.apply(fn), which will apply `fn` recursively to every submodule (as returned by `.children()`) as well as self. Typical use includes initializing the parameters of a model.

```python
if isinstance(m, nn.Conv2d):
    ...
# or
if type(m) == nn.Conv2d:
    ...
```

