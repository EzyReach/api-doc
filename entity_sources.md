# Entity Sources

There are three sources of information:
1. User - The data to be entered by the user manually
2. GST - The data that is fetched from the GST portal using user's GSTIN
3. LSP - The data that the LSP itself is providing

## 1. User Onboarding

|Fields   |Source|Comment|
|---------|:----:|:------|
|username |USER  |username is same as user's email|
|password |USER  |
|mobile   |USER  |


## 2. User profiling

|Fields        |Source|Comment|
|--------------|:----:|:------|
|gstin         |USER  ||
|primary id    |Unknown|Either USER or GST|
|Contact detail|Unknown|Either USER or GST|