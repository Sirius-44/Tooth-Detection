# Dental 3D
统一结构（nnU-Net）
```
DATASET_NAME/
├── imagesTr/          # 训练体积（.nii.gz / .mha / .npy 等，建议转为 .nii.gz）
├── labelsTr/          # 对应分割标签（与 imagesTr 一一对应）
├── imagesTs/          # 测试体积（如官方提供或自划分）
├── labelsTs/          # 测试标签（若公开）
└── dataset.json       # 含模态、spacing、类别映射等元信息
``````
*原始数据为 .mha/.npy/DICOM，建议统一转换为 .nii.gz，便于跨工具链（nnU-Net / MONAI / 3D U-Net 等）使用。*

## 1.ToothFairy
**数据特征**：
- **数据特点**：ToothFairy 是一个基于 CBCT（Cone-Beam CT）体积数据的牙科数据集，主要用于 下牙槽管（Inferior Alveolar Canal, IAC）分割任务。
数据以 .npy 格式保存，提供了 dense（全体素标注）与 sparse（稀疏点/结构标注）两种标注模式，便于研究全监督与半监督分割算法。
- **数据规模**：体积：若干卷 CBCT 体积（平均维度约 169×342×370 voxels）。类别数：单类别（IAC 通道结构）
- **应用方向**：下牙槽神经自动分割与追踪

**文件结构与下载方式**：
````
ToothFairy/
├── imagesTr/       # CBCT 体积（.npy 或转换为 .nii.gz）
├── labelsTr/       # 分割掩码
└── dataset.json
``````
[数据集地址](https://ditto.ing.unimore.it/toothfairy/)
**相关研究**：

## 2.ToothFairy2
**数据特征**：
- **数据特点**：ToothFairy2 是 ToothFairy 的升级版本，包含 42 类牙科结构（牙齿、颌骨、上颌窦、桥体、牙冠、种植体等）。
它以 .mha 格式提供，结构遵循 nnU-Net 约定，可直接用于 3D 分割模型训练。
- **数据规模**：数据量：Set A：417 卷（文件名前缀 “P…”）;Set B：63 卷（文件名前缀 “F…”）
体积范围：最大 298×512×512，最小 170×272×345
类别数：42 类
格式：MetaImage (.mha)
- **应用方向**：多结构三维语义分割/颌面重建、全口牙模型生成

**文件结构与下载方式**：
````
ToothFairy2/
├── imagesTr/    # 分割掩码
└── dataset.json
``````
[数据集地址](https://ditto.ing.unimore.it/toothfairy2/)

**相关研究**：ToothFairy2: Multi-class CBCT Dataset for 3D Dental Anatomy Segmentation

## 3.ToothFairy3
**数据特征**：
- **数据特点**：ToothFairy3 是目前最完整的 ToothFairy 系列数据集，包含 77 类结构标注，新增如牙髓腔（pulp cavity）、左右切牙管、舌下管等细微结构。
采用 .nii/.nii.gz 格式，保持高空间一致性，适合进行复杂三维器官与微结构建模。
- **数据规模**：
数据量：Set A：417 卷（文件名前缀 “P…”）;Set B：63 卷（文件名前缀 “F…”）;Set C：52 卷
体积范围：最大 298×512×512，最小 170×272×345
类别数：77 类
格式：NIfTI (.nii, .nii.gz)
- **应用方向**：全颌高精度结构分割、微结构三维重建与生成模型预训练

**文件结构与下载方式**：
````
ToothFairy3/
├── imagesTr/  
├── labelsTr/  
└── dataset.json
``````
[数据集地址](https://ditto.ing.unimore.it/toothfairy3/)

**相关研究**：ToothFairy3 已被广泛用于 3D Transformer 与 Foundation Model 的训练，例如 OralGPT、MMOral 和 STS3DTooth 预训练工作，
NeurIPS 2025 论文中使用其作为多模态结构数据源之一。

## 4.STS3DTooth
**数据特征**：
- **数据特点**：STS3DTooth 是一个多模态牙科影像数据集，包含 CBCT 体积、部分标注以及大量未标注样本。旨在支持 自监督预训练、半监督学习和跨模态建模，数据来源于多机构临床扫描。
- **数据规模**：
数据量：148,400 个未标记扫描和 8,800 个掩模。
体积范围：典型体积约 200×400×400 voxels
类别数：77 类
数据模态：CBCT + 模拟数据
格式：NIfTI (.nii.gz) 或 DICOM
- **应用方向**：自监督/半监督学习、3D-to-3D Domain Adaptation

**文件结构与下载方式**：
````
STS3DTooth/
├── imagesTr/     # 标注样本
├── labelsTr/
├── imagesUl/     # 未标注数据
└── dataset.json
``````
[数据集地址](https://zenodo.org/records/10597292)
**相关研究**：[Nature Scientific Data (2024)](https://www.nature.com/articles/s41597-024-04306-9)
它被 OralGPT 等多模态模型用作预训练基座，用于 3D 医学影像语义理解。

## 5.CTooth
**数据特征**：
- **数据特点**：CTooth 是一个专注于 3D 牙齿体积分割的标准基准数据集。
提供高质量人工标注样本，并评估多种 3D 网络（如 UNet、VNet、PointNet++）。
- **数据规模**：22 个精注释体积 + 约 146 个未标注体积大小：约 160×320×320 voxels
类别数：牙齿/背景（可拓展）
格式：NIfTI (.nii.gz)
- **应用方向**：单牙或全牙体积分割

**文件结构与下载方式**：
````
CTooth/
├── imagesTr/
├── labelsTr/
├── imagesUl/
└── dataset.json
``````
[数据集地址](https://github.com/liangjiubujiu/CTooth)

**相关研究**：论文 “CTooth: Benchmark for 3D Tooth Segmentation” (arXiv:2206.08778)
提出该数据集并系统评估了主流 3D 网络，是牙齿体积分割研究的重要对比标准。

## 6.Teeth3DS
**数据特征**：
- **数据特点**：包含 120 个高分辨率牙齿扫描（STL/PLY 格式），用于牙齿表面网格建模与重建。
- **数据规模**：120 例 | 网格分辨率平均 >100k vertices。
格式：STL/PLY 格式
- **应用方向**：3D 重建、几何分割、正畸分析。

**下载方式**：
[数据集地址](https://github.com/johnson444/Teeth3DS)

**相关研究**：常用于 PointNet++、MeshCNN 等几何网络评测。

## 7.Oral3D (MandSeg3D)
**数据特征**：
- **数据特点**：以 CT/CBCT 扫描为基础的颌骨与牙齿联合分割数据集。
- **数据规模**：200+ 例 CT 扫描 | 分辨率约 512×512×300。
格式：CT/CBCT
- **应用方向**：颌面骨重建、3D 配准、手术导航。

**下载方式**：
[数据集地址](https://github.com/Oral3D/MandSeg3D)

**相关研究**：用于深度颌骨分割算法基准（Oral3D Challenge）。

## 8.Cephalometric3D
**数据特征**：
- **数据特点**：3D 头颅 X 光重建与标注点数据集。
- **数据规模**：300 例 CBCT 扫描 + 标注点坐标。
格式：CT/CBCT
- **应用方向**：颅面结构检测、关键点定位、正畸辅助分析。

**下载方式**：
[数据集地址](https://www.kaggle.com/datasets/)

**相关研究**：用于 Landmark Detection 与 Pose Estimation 模型训练。

## 其余数据集
![Alt text](image.png)

# Dental 2D

## 1.DENTEX √
**数据信息**：
- **数据特点**：数据集分为三类，第一类划分牙齿的四象限；第二类划分牙齿象限内牙号，第三类，将裁剪的全景影像区域分为四类牙齿异常类型：龋齿、深龋齿、阻生牙和根尖周围病变。

| Classes |疾病|
| -----| -----|
|0|Caries|
1| 深龋齿
2|impacted
3|根尖周围病变
- **数据规模**：第一类：693例；第二类：634例；第三类705例; 无标签：1571例；验证集（无标签）：50例

- **格式**：标注：JSON 标注格式，包含：牙号、象限、疾病标签、bbox。影像：大小约2880*1316、png
- **应用方向**：牙齿检测、口腔疾病诊断

**下载地址**：[数据集地址](https://dentex.grand-challenge.org/dentex/)

**相关论文**：Combining public datasets for automated tooth assessment in panoramic radiographs

## 2.DXPD √
**数据信息**：

- **数据特点**：全景图像区域划分为31种牙齿异常类型：龋齿、种植体、缺牙、骨量减少、囊肿等。

| Classes |疾病|
| -----| -----|
|0|Caries
1| Crown
2| Filling
3| Implant
4| Malaligned
5| Mandibular Canal
6| Missing teeth
7| Periapical lesion
8| Retained root
9| Root Canal Treatment
10| Root Piece
11| Impacted tooth
12| Maxillary sinus
13| Bone Loss
14| Fracture teeth
15| Permanent Teeth
16| Supra Eruption
17| TAD
18| Abutment
19| Attrition
20| Bone defect
21| Gingival former
22| Metal band
23| Orthodontic brackets
24| Permanent retainer
25| Post-core
26| Plating
27| Wire
28| Cyst
29| Root resorption
30| Primary teeth
- **数据规模**：train：9481例；val:2871例；test：1580例

- **格式**：coco和yolo格式；图像大小640、jpg
- **应用方向**：疾病检测

**下载地址**：[数据集地址](https://www.kaggle.com/datasets/lokisilvres/dental-disease-panoramic-detection-dataset?resource=download)

**相关论文**：暂无（应该有，下载了权重文件）

## 3.DXPD √
**数据信息**：
- **数据特点**：全景图像区域分为4种牙齿异常类型：龋齿、充填物、阻生牙和种植体

| Classes |疾病|
| -----| -----|
|0|cavity
1| impacted
2| Filling
3| Implant（种植体）

- **数据规模**： 1075|121|73例

- **格式**：标注：csv标注格式；影像：大小512*256、jpg
- **应用方向**：疾病检测

**下载地址**：[数据集地址](https://www.kaggle.com/datasets/imtkaggleteam/dental-radiography)

**相关论文**：无

**备注**：图像是椭圆

## 4.DC1000 √
**数据信息**：
- **数据特点**：全景片中龋齿的严重程度分为3类：轻度、中度和重度。

- **数据规模**： 

- **格式**：标注：；影像：
- **应用方向**：龋齿检测

**下载地址**：[数据集地址](https://github.com/Zzz512/MLUA?tab=readme-ov-file)

**相关论文**：无

## 5.OdontoAI √
**数据信息**：
- **数据特点**：牙齿分割及对应的FDI编号（覆盖了全部恒牙和乳牙，共计52个类别）

- **数据规模**： 1533|286例

- **格式**：标注：coco格式（检测和分割标注都有）；影像：1292*2440、jpg
- **应用方向**：牙齿检测

**下载地址**：[数据集地址](https://universe.roboflow.com/evident-mybn8/odontoai/dataset/1)

**相关论文**：
- OdontoAI: A human-in-the-loop labeled data set and an online platform to boost research on dental panoramic radiographs

- Combining public datasets for automated tooth assessment in panoramic radiographs

## 6.Periapical X-rays √
**数据信息**：
- **数据特点**：五类牙根尖周与牙周联合病变类型（仅有类别标签）

- **数据规模**：

| Classes |nunber|
| -----| -----|
|原发性牙髓病变伴继发性牙周病变|122
原发性牙髓病变| 124
原发性牙周病变伴继发性牙髓病变| 39
原发性牙周病变| 118
真性联合病变| 131

- **格式**：标注：仅有类别标签；影像：约796*611、jpg
- **应用方向**：牙根周疾病检测

**下载地址**：[数据集地址](https://www.kaggle.com/datasets/muhammadsajad/periapical-xrays/data)

**相关论文**：
无

## 7.TSDX √
**数据信息**：
- **数据特点**：人工标注的高精度牙齿分割数据集，32类，编号是按顺序编号，不是FDI

- **数据规模**：591例

- **格式**：标注：Supervisely JSON格式（用于语义分割）；影像：1024*2041、jpg
- **应用方向**：牙齿检测

**下载地址**：[数据集地址](https://www.kaggle.com/datasets/humansintheloop/teeth-segmentation-on-dental-x-ray-images)

**相关论文**：
无

## 8.STS-2D
**数据信息**：
- **数据特点**：从全景片中对成人牙齿进行二值分割。（数据量很大）

- **数据规模**：

- **格式**：标注格式：；影像大小：；影像格式：
- **应用方向**：

**下载地址**：[数据集地址](https://echoyq.github.io/ToothFairlySSS/)

**相关论文**：

## 9.CDPRD
**数据信息**：
- **数据特点**：从全景片中对儿童牙齿进行二值分割。

- **数据规模**：

- **格式**：标注格式：；影像大小：；影像格式：
- **应用方向**：

**下载地址**：[数据集地址](https://springernature.figshare.com/collections/Children_s_Dental_Panoramic_Radiographs_Dataset_for_Caries_Segmentation_and_Dental_Disease_Detection/6317013/1)

**相关论文**： Children’s dental panoramic radiographs dataset for caries segmentation and dental disease detection

## 10.ADLD
**数据信息**：
- **数据特点**：从全景片中分割出单个牙齿并对其进行标记。

- **数据规模**：

- **格式**：标注格式：；影像大小：；影像格式：
- **应用方向**：

**下载地址**：[数据集地址](https://www.kaggle.com/datasets/zwbzwb12341234/a-dual-labeled-dataset)

**相关论文**：

## 11.TSD-FG
**数据信息**：
- **数据特点**：对每个牙齿、牙本质、牙髓、牙科材料和龋坏进行细粒度分割。

- **数据规模**：

- **格式**：标注格式：；影像大小：；影像格式：
- **应用方向**：

**下载地址**：[数据集地址](https://github.com/Zzz512/TSD)

**相关论文**：

## 12.Tufts
**数据信息**：
- **数据特点**：从全景图像中分割出异常区域。

- **数据规模**：

- **格式**：标注格式：；影像大小：；影像格式：
- **应用方向**：

**下载地址**：[数据集地址](https://tdd.ece.tufts.edu/)

**相关论文**： 

## 13.caries-Xrays
**数据信息**：
- **数据特点**：从全景图像中分割龋齿。

- **数据规模**：6000例

- **格式**：标注格式：VOC；影像大小：2648*1280；影像格式：jpg
- **应用方向**：龋齿检测

**下载地址**：[数据集地址]（https://github.com/Binz-Chen/AAAI2024_CariesXrays）

**相关论文**：CariesXrays: Enhancing Caries Detection in Hospital-Scale Panoramic Dental X-rays via Feature Pyramid Contrastive Learning

***

## 14.Panoramic radiographs with periapical lesions Dataset
**数据信息**：

- **数据特点**：

- **数据规模**：

- **格式**：标注格式：；影像大小：；影像格式：
- **应用方向**：

**下载地址**：[数据集地址](https://data.mendeley.com/datasets/kx52tk2ddj/3)

**相关论文**：

***

## 15.PerioXrays

**数据信息**：

- **数据特点**：

- **数据规模**：

- **格式**：标注格式：；影像大小：；影像格式：
- **应用方向**：

**下载地址**：[数据集地址](https://huggingface.co/datasets/XiaochengFang/PerioXrays)

**相关论文**：PerioDet: Large-Scale Panoramic Radiograph Benchmark for Clinical-Oriented Apical Periodontitis Detection

***

## 16.Dental X Ray Computacional Vision Segmentation

**数据信息**：

- **数据特点**：

- **数据规模**：

- **格式**：标注格式：；影像大小：；影像格式：
- **应用方向**：

**下载地址**：[数据集地址](https://www.kaggle.com/datasets/henriquerezermosqur/dental-x-ray-computacional-vision-segmentation/data)

**相关论文**：
