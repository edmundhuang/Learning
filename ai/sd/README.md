### Install
1. 安装 python V3.10.6
2. Git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git
3. Run webui-user.bat in "ui" folder.  2023-04-25 12:29PM
4. 

### Exceptions
1. 没有Nvidia 显卡
AssertingError: Torch is not able to use GPU; add --skip-torch-cuda-test to COMMANDLINE_ARGS variable to disable this check
2. 没有GPU，只是用CPU
add --precision full --no-half to COMMANDLINE_ARGS

