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
每一种算法训练的模型分别放置在当前目录下SKL_HGB，XGBoost和Roost文件夹下。每个算法文件夹都包含以下几个子文件夹：
- **Seebeck_n**（预测n型泽贝克系数模型）
- **Seebeck_p**（预测p型泽贝克系数模型）
- **ElecCond**（预测电导率模型）
- **ThermCond**（预测热导率模型）
- **PF**（预测功率因子模型）
- **ZT**（预测热电优值模型）

每个子文件夹中包含有训练好的模型文件和调用脚本。
### SKL_HGB模型使用方法
以热电优值模型为例（**ZT**）:

**输入**：.csv文件，如test.csv，格式如下表所示
| index         | composition                  | temp             |
| --------------- | ------------------------ | -------------------- |
| 0 | Nd0.8Ca0.2BaCo2O5.5      | 300     |
| 1 | Nd0.8Ca0.2BaCo2O5.5      | 400     |
| 2 | Mg2.08Si0.352Sn0.6Sb0.048      | 300     |
| 3 | Mg2.08Si0.352Sn0.6Sb0.048      | 400     |
| ...... | ...... | ...... |

**运行**：
```sh
python gen_feature.py
python predict.py
```

**输出**：.csv文件，如predict.csv，格式如下表所示
| index         | composition                  | temp             | Pred_HGB |
| --------------- | ------------------------ | -------------------- | -------------------- |
| 0 | Nd0.8Ca0.2BaCo2O5.5      | 300     | 0.2      |
| 1 | Nd0.8Ca0.2BaCo2O5.5      | 400     | 0.3      |
| 2 | Mg2.08Si0.352Sn0.6Sb0.048      | 300     | 0.1      |
| 3 | Mg2.08Si0.352Sn0.6Sb0.048      | 400     | 0.2      |
| ...... | ...... | ...... | ...... |

### XGBoost模型使用方法
以热电优值模型为例（**ZT**）:

**输入**：.csv文件，如test.csv，格式如下表所示
| index         | composition                  | temp             |
| --------------- | ------------------------ | -------------------- |
| 0 | Nd0.8Ca0.2BaCo2O5.5      | 300     |
| 1 | Nd0.8Ca0.2BaCo2O5.5      | 400     |
| 2 | Mg2.08Si0.352Sn0.6Sb0.048      | 300     |
| 3 | Mg2.08Si0.352Sn0.6Sb0.048      | 400     |
| ...... | ...... | ...... |

**运行**：
```sh
python gen_feature.py
python predict.py
```

**输出**：.csv文件，如predict.csv，格式如下表所示
| index         | composition                  | temp             | Pred_XGB |
| --------------- | ------------------------ | -------------------- | -------------------- |
| 0 | Nd0.8Ca0.2BaCo2O5.5      | 300     | 0.2      |
| 1 | Nd0.8Ca0.2BaCo2O5.5      | 400     | 0.3      |
| 2 | Mg2.08Si0.352Sn0.6Sb0.048      | 300     | 0.1      |
| 3 | Mg2.08Si0.352Sn0.6Sb0.048      | 400     | 0.2      |
| ...... | ...... | ...... | ...... |

### Roost模型使用方法
以热电优值模型为例（**ZT**）:

**输入**：.csv文件，如test.csv，格式如下表所示
| material_id         | composition                  | temp             |
| --------------- | ------------------------ | -------------------- |
| 0 | Nd0.8Ca0.2BaCo2O5.5      | 300     |
| 1 | Nd0.8Ca0.2BaCo2O5.5      | 400     |
| 2 | Mg2.08Si0.352Sn0.6Sb0.048      | 300     |
| 3 | Mg2.08Si0.352Sn0.6Sb0.048      | 400     |
| ...... | ...... | ...... |

**运行**：
```sh
python roost-example.py --evaluate --test-path test.csv --targets y --tasks regression --losses L2 --data-seed 42 --ensemble 1 --batch-size 256 --model-name ZT_1 --run-id 1 --log
```

注：每个性质的命令稍有不同，区别在于--model-name选择不同的性质对应的模型。具体参见每个性质文件夹中的jobscript文件。

**输出**：.csv文件，如predict.csv，格式如下表所示
| material_id         | composition                  | temp             | Pred_Roost |
| --------------- | ------------------------ | -------------------- | -------------------- |
| 0 | Nd0.8Ca0.2BaCo2O5.5      | 300     | 0.2      |
| 1 | Nd0.8Ca0.2BaCo2O5.5      | 400     | 0.3      |
| 2 | Mg2.08Si0.352Sn0.6Sb0.048      | 300     | 0.1      |
| 3 | Mg2.08Si0.352Sn0.6Sb0.048      | 400     | 0.2      |
| ...... | ...... | ...... | ...... |
