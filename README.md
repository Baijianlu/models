# models
This project contains pretrained ML models to predict thermoelectric transport properties only using composition and temperature.
## 安装
模型依赖于scikit-learn，XGBoost，pytorch等软件包训练和使用，在调用模型之前需要安装这些依赖的软件。
对于SKL_HGB和XGBoost模型，执行以下命令安装依赖环境：
```sh
pip install -r requirements.txt
```
对于Roost模型，先执行以下命令安装依赖库：
```sh
git clone https://github.com/CompRhys/aviary
pip install -e ./aviary
```
然后进入aviary实际安装所在的python库文件夹中（如~/anaconda3/lib/python3.12/site-packages/），用当前目录下的**aviary**文件夹替换掉python库文件夹中的**aviary**（因为我对一些关键的文件进行了修改）。同时把当前目录下的**models**文件夹拷贝到python库文件夹中和**aviary**同级。
## 调用
