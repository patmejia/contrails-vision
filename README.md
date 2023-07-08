#### Title:
# GOES-16 Satellite Contrail Detection using CV/ML

##### Optimizing satellite imagery, [GOES-R ABI](https://www.star.nesdis.noaa.gov/goes/index.php), and advanced computer vision/machine learning for accurate detection of contrails


#### Absract:
##### The "OpenContrails: Benchmarking Contrail Detection" paper proposes a new contrail detection model, enhancing the study of climate change. The model, leveraging multiple frames for temporal context, improves detection performance and focuses on young, linear contrails. It utilizes the OpenContrails dataset, containing human-labeled contrail detections from the GOES-16 satellite, and confirms prior contrail research. The authors present the OpenContrails dataset and model as public benchmarks, promoting advances in contrail research. This work involves contributors from Google's Research Department and MIT's Laboratory for Aviation and the Environment.

![network-architecture](documentation/images/network-architecture.png)

> #### Q: Why focus on contrails to curb climate change impacts?
> #### Adam Durant: It’s not just direct engine emissions that matter in terms of aviation’s climate impacts. Non-carbon dioxide sources — like the climate forcing from contrails — make up almost two-thirds of the industry’s impact, which is a surprisingly big number. In fact, it equates to 2% of all human-caused climate change.
![detected-contrails-flights](documentation/images/detected-contrails-flights.png)

#### Dataset: OpenContrails

#### Dataset description:
##### ☛ OpenContrails is a dataset of contrail detections from GOES-16 Advanced Baseline Imager data. <br> ☛ Created to train models for contrail detection and climate impact assessment. <br> ☛ Focuses on young, linear-shaped contrails due to climate change contribution. <br> ☛ Contains high-quality per-pixel contrail masks for each image. <br> ☛ Includes contrail detection model output from multiple years of GOES-16 images. <br> ☛ Images are derived from GOES-16 ABI in geostationary orbit. <br> ☛ Covers North and South American region with 10-minute interval images since April 2019. <br> ☛ Examples generated by random sampling of GOES-16 viewable extent from April 2019-2020. <br> ☛ Samples restricted within -50 to 50-degree latitude and -135 to -30-degree longitude. <br> ☛ Contrail detection model uses deep neural networks, including ResNet and DeeplabV3+ architectures. <br> ☛ Dataset and outputs are publicly available on Google Cloud Storage [bucket: gcp-public-data-goes-16](https://console.cloud.google.com/storage/browser/gcp-public-data-goes-16;tab=objects?prefix=&forceOnObjectsSortingFiltering=false).

#### ☛ Documentation: [research.md](documentation/RESEARCH.md)

## ➲ Setup

#### ☛ option 1: using `conda`
```bash
conda env create -f requirements.yml
conda activate contrail_env
```

#### ☛ option 2: using `pip` and `venv`
```bash
python -m venv contrails_env
source contrails_env/bin/activate
pip install -r requirements.txt
```
#### ☛ option 3: using `conda` and `pip` ?
```bash
conda create -n contrail_env
conda activate contrail_env
pip install -r requirements.txt
```
Both `conda`` and `pip`` can be used in the same environment, but issues may arise. Using them back-to-back can create an unreproducible state and overwrite packages. To avoid problems, create an isolated conda environment, install most packages with conda, and use pip with `--upgrade-strategy only-if-needed`.

---
### Kaggle api key (optional)
```bash
pip install kaggle
mkdir ~/.kaggle
mv /path/to/kaggle.json ~/.kaggle/kaggle.json
chmod 600 ~/.kaggle/kaggle.json
kaggle competitions list
```
##### ☛ Install the Kaggle CLI <br> ☛ Create a Kaggle account and go to your account settings page. <br> ☛ Click "Create New API Token" to download the `kaggle.json` file  <br> ☛  Move the downloaded file to `~/.kaggle/kaggle.json` <br> ☛ Set permissions for the API key file <br> ☛ Confirm the setup: Run kaggle competitions list to verify the API key works
---
### Download data (optional)
##### ☛ sample-dataset ▸ ash-color [22.4k files - 11.74 GB](https://www.kaggle.com/shashwatraman/contrails-images-ash-color)
```bash 
kaggle datasets download shashwatraman/contrails-images-ash-color -p /path/to/desired/directory
unzip contrails-images-ash-color.zip -d /path/to/desired/directory
rm contrails-images-ash-color.zip
```
##### ☛ full-dataset  ▸  OpenContrails [244.4k files - 450.91 GB](https://arxiv.org/pdf/2304.02122.pdf)

```bash
kaggle competitions download -c google-research-identify-contrails-reduce-global-warming
```
---

## ➲ Run
```bash
conda activate contrail_env 
pytest -sv
python src/main.py
```

#### Stop
```bash
conda deactivate
```
---
### Acknowledgements:

```bibtex
@article{ng2023opencontrails,
  title={OpenContrails: Benchmarking Contrail Detection on GOES-16 ABI},
  author={Ng, Joe Yue-Hei and McCloskey, Kevin and Cui, Jian and Meijer, Vincent and Brand, Erica and Sarna, Aaron and Goyal, Nita and Van Arsdale, Christopher and Geraedts, Scott},
  journal={arXiv preprint arXiv:2304.02122},
  year={2023}
}
```
##### 📓 arxiv: https://arxiv.org/abs/2304.02122
##### [🔢 goes_contrails_dataset from OpenContrails: Benchmarking Contrail Detection on GOES-16 ABI](https://console.cloud.google.com/storage/browser/goes_contrails_dataset%253Btab%253Dobjects?prefix%253D%2526forceOnObjectsSortingFiltering%253Dfalse)
<a href="https://www.kaggle.com/competitions/google-research-identify-contrails-reduce-global-warming" target="_blank"><img align="left" alt="Kaggle" title="Open competition in Kaggle" src="https://kaggle.com/static/images/open-in-kaggle.svg"></a>
<br>
---
##### ☛ contrails-labeling-guide: https://storage.googleapis.com/goes_contrails_dataset/20230419/Contrail_Detection_Dataset_Instruction.pdf
##### 🄺 contrails dataset sample (11.74 GB) train_df.csv, valid_df.csv: https://www.kaggle.com/datasets/shashwatraman/contrails-images-ash-color
##### 🄺 visualize (input dataset 450.91 GB): https://www.kaggle.com/code/inversion/visualizing-contrails#OpenContrails-dataset-documentation
##### 🄺 high-score-example: https://www.kaggle.com/code/egortrushin/gr-icrgw-training-with-4-folds
##### 🄺 Using U-Net to Predict Segmentation Masks in Python & Keras: https://www.kaggle.com/keegil/keras-u-net-starter-lb-0-277
----
##### 🐍 Using Python to Explore GOES-16 Data: https://edc.occ-data.org/goes16/python/
##### 🌍 visualization: [RAMMB CIRA, colostate.edu](https://rammb-slider.cira.colostate.edu/?sat=goes-18&sec=full_disk&x=12480&y=9274.5&z=0&angle=0&im=12&ts=1&st=0&et=0&speed=130&motion=loop&maps%5Bborders%5D=white&p%5B0%5D=geocolor&opacity%5B0%5D=1&pause=0&slider=-1&hide_controls=0&mouse_draw=0&follow_feature=0&follow_hide=0&s=rammb-slider&draw_color=FFD700&draw_width=6)
##### ☛ [STAC](https://stacspec.org/en/tutorials/1-read-stac-python/)
##### ☛ [WGS84 coordinate system](https://support.virtual-surveyor.com/en/support/solutions/articles/1000261351-what-is-wgs84-)
---
##### 🔢 gcp-public-data-goes-16: https://console.cloud.google.com/storage/browser/gcp-public-data-goes-16;tab=objects?prefix=&forceOnObjectsSortingFiltering=false
##### ☛ Beginner's Guide to GOES-R Series Data: https://www.goes-r.gov/downloads/resources/documents/Beginners_Guide_to_GOES-R_Series_Data.pdf
##### ☛ GOES-R Series Product Definition and users' guide: [Level 2+ Algorithm Products, page 43](https://www.goes-r.gov/products/docs/PUG-L2+-vol5.pdf)
##### ☛ GOES-16 (Geostationary Operational Environmental Satellite, Launch Date: Nov. 19, 2016): https://eospso.nasa.gov/missions/geostationary-operational-environmental-satellite-16
##### ☛ GOES-16 Band Reference Guide: https://www.weather.gov/media/crp/GOES_16_Guides_FINALBIS.pdf
##### ☛ Adam Duran (Michigan Tech, Q&A with SATAVIA: Climate and Contrails): https://www.mtu.edu/unscripted/2021/06/qa-with-satavia-climate-and-contrails.html
##### ☛ catalogues of atmospheric optics (rocket plume, contrail shadow): https://atoptics.co.uk/atoptics/shuttle.htm, https://atoptics.co.uk/atoptics/contr1.htm
##### 📓  U-Net: Convolutional Networks for Biomedical Image Segmentation: https://arxiv.org/abs/1505.04597
---
##### [🗑️ paper with code: opencontrails-benchmarking-contrail-detection ](https://paperswithcode.com/paper/opencontrails-benchmarking-contrail-detection)
---


### Contributing
#### 👋 Welcome to the contributing section! We're excited to have you join us in enhancing the GOES-16 Satellite Contrail Detection project. Contribute by forking the repository, making changes in a descriptive branch, and submitting a pull request. Join our [Slack](https://sdteam6.slack.com/archives/C05D6MBTW2D) channel for real-time communication with other contributors. Follow and contribute to this impactful project to combat climate change through advanced technology 🌍✨