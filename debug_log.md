
# Debug log while installation

## Dependencies

Numpy
- the original requirements.txt doesn't specify numpy version.
- manually installed numpy-12.3

pytorch
- torch-1.7.1 doesn't work on my PC with RTX 3090 with capability sm_86
- see relevant issue: https://discuss.pytorch.org/t/geforce-rtx-3090-with-cuda-capability-sm-86-is-not-compatible-with-the-current-pytorch-installation/123499
- I manually installed torch for cuda12

(possible) missing dependency packaging
- manually installed packaging=21.3
- relevant with this issue:  [Try to run 'quickstart' and meet the bug: Invalid version: '0.10.1,<0.11'](https://github.com/cliport/cliport/issues/20)

## issues in clip.py

### Line 567, 
```
if "value" in node.attributeNames() and str(node["value"]).startswith("cuda"):
```

change jit=True to False in line 534

### Line 491, 
```
File "/home/fan/GitHub/cliport/cliport/models/core/clip.py", line 491, in build_model
del state_dict[key]
KeyError: 'input_resolution'
```

This issue is because the key "input_resolution" is not in the state_dict, simply add a checking before executing the next del operation.

