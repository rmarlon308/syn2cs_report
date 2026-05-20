# Cityscapes vs SYNTHIA Dataset Comparison

This report presents metrics for the DAFormer model trained on SYNTHIA (source) and evaluated on Cityscapes (target). Metrics were obtained by evaluating the trained model on the Cityscapes validation set (3 cities, 500 images) and on a 500-image subset of SYNTHIA.

## View Examples

The following images illustrate the appearance and field-of-view of the Cityscapes and SYNTHIA datasets.

| Cityscapes | Synthia |
|-----------|-----------|
| ![cs_example](assets/cityscapes/leftImg8bit/val/frankfurt/frankfurt_000000_006589_leftImg8bit.png) | ![syn_example](assets/synthia_subset_500/RGB/0003258.png) |
| ![cs_example1](assets/cityscapes/leftImg8bit/val/lindau/lindau_000007_000019_leftImg8bit.png) | ![syn_example1](assets/synthia_subset_500/RGB/0001326.png) |  


## Whole-Image Statistics

The table below shows mIoU and average global error for Cityscapes and SYNTHIA. mIoU shows an approximate 15% gap, while average global error differs by about 6.5%.

Definitions:
- mIoU: For calculating the mIoU, pixels are aggregated across all images and IoU is computed over all pixels combined.
- Average Global Error: the mean per-image pixel error (excluding ignored pixels).

| Metric | Cityscapes | SYNTHIA |
|---|---:|---:|
| mIoU | 61.20% | 76.09% |
| Average Global Error | 11.54% | 4.98% |

### 4x4 Grid Analysis

Each image is divided into a 4x4 grid. The plot below shows the error for each grid cell computed over 500 images for Cityscapes and SYNTHIA.

There is a strong spatial mismatch between the datasets: Cityscapes and SYNTHIA exhibit opposite error patterns. In Cityscapes, errors concentrate in the lower half of the image (rows 2–3). In SYNTHIA the bottom row is highly reliable, and the most difficult regions for small objects appear in the upper and middle rows.


![4x4 Grid Analysis](assets/image.png)



<!-- | Cityscpes | Synthia |
|-----------|-----------|
| ![example_cs](assets/synthia_subset_500/frankfurt_000001_075296_leftImg8bit.png) | ![example_syn](assets/synthia_subset_500/RGB/0000268.png) |
 -->

### 4x4 Grid by Class: Spatial Error Distribution by Representation (Top 5)

The following tables show the top 5 most represented classes (with their errors) for each cell of the grid for Cityscapes and Synthia.

| Cityscapes | Col 0 | Col 1 | Col 2 | Col 3 |
|:---:|:---:|:---:|:---:|:---:|
| Row 0 | Building (51.12%) (Err: 3.81%)<br>Vegetation (38.06%) (Err: 4.36%)<br>Sky (6.72%) (Err: 0.88%)<br>Pole (1.71%) (Err: 29.03%)<br>Traffic sign (1.01%) (Err: 12.87%) | Vegetation (40.08%) (Err: 4.37%)<br>Building (37.02%) (Err: 3.32%)<br>Sky (20.73%) (Err: 0.87%)<br>Pole (1.09%) (Err: 42.56%)<br>Traffic sign (0.45%) (Err: 14.71%) | Vegetation (40.22%) (Err: 4.05%)<br>Building (40.15%) (Err: 3.52%)<br>Sky (16.50%) (Err: 1.24%)<br>Pole (1.33%) (Err: 41.56%)<br>Traffic sign (1.00%) (Err: 12.11%) | Building (56.22%) (Err: 3.64%)<br>Vegetation (34.43%) (Err: 3.91%)<br>Sky (3.24%) (Err: 1.42%)<br>Traffic sign (2.34%) (Err: 14.18%)<br>Pole (1.91%) (Err: 30.60%) |
| Row 1 | Building (39.89%) (Err: 7.54%)<br>Vegetation (24.02%) (Err: 6.53%)<br>Car (15.95%) (Err: 2.90%)<br>Pole (3.37%) (Err: 32.37%)<br>Person (3.13%) (Err: 12.46%) | Building (30.63%) (Err: 9.21%)<br>Vegetation (27.76%) (Err: 5.98%)<br>Car (14.61%) (Err: 4.03%)<br>Road (8.90%) (Err: 10.49%)<br>Person (3.77%) (Err: 12.46%) | Building (29.88%) (Err: 9.66%)<br>Vegetation (26.20%) (Err: 6.00%)<br>Car (14.49%) (Err: 4.45%)<br>Road (8.63%) (Err: 11.64%)<br>Person (4.28%) (Err: 12.44%) | Building (38.37%) (Err: 8.12%)<br>Vegetation (21.64%) (Err: 7.04%)<br>Car (15.25%) (Err: 3.49%)<br>Fence (4.33%) (Err: 95.56%)<br>Person (4.06%) (Err: 11.70%) |
| Row 2 | Road (58.66%) (Err: 7.27%)<br>Sidewalk (14.69%) (Err: 14.28%)<br>Car (13.74%) (Err: 4.63%)<br>Vegetation (3.03%) (Err: 22.88%)<br>Building (2.74%) (Err: 21.79%) | Road (86.25%) (Err: 8.83%)<br>Sidewalk (5.02%) (Err: 16.04%)<br>Car (3.98%) (Err: 7.53%)<br>Person (1.13%) (Err: 9.65%)<br>Vegetation (0.92%) (Err: 36.29%) | Road (84.05%) (Err: 9.23%)<br>Sidewalk (7.86%) (Err: 13.21%)<br>Car (4.00%) (Err: 7.77%)<br>Person (1.11%) (Err: 9.05%)<br>Building (0.79%) (Err: 15.10%) | Road (43.85%) (Err: 8.74%)<br>Sidewalk (28.70%) (Err: 13.39%)<br>Car (14.03%) (Err: 4.28%)<br>Building (3.56%) (Err: 13.50%)<br>Vegetation (3.03%) (Err: 28.83%) |
| Row 3 | Road (92.34%) (Err: 20.63%)<br>Sidewalk (4.59%) (Err: 8.45%)<br>Car (1.82%) (Err: 9.74%)<br>Vegetation (0.44%) (Err: 48.89%)<br>Wall (0.41%) (Err: 18.41%) | Road (99.43%) (Err: 23.80%)<br>Sidewalk (0.52%) (Err: 9.75%)<br>Person (0.04%) (Err: 5.64%)<br>Car (0.01%) (Err: 9.70%)<br>Vegetation (0.01%) (Err: 100.00%) | Road (99.44%) (Err: 23.46%)<br>Sidewalk (0.43%) (Err: 31.96%)<br>Car (0.08%) (Err: 44.97%)<br>Person (0.06%) (Err: 3.22%) | Road (84.89%) (Err: 19.01%)<br>Sidewalk (12.70%) (Err: 10.54%)<br>Car (1.65%) (Err: 11.61%)<br>Vegetation (0.40%) (Err: 38.36%)<br>Fence (0.13%) (Err: 46.53%) |

Cityscapes analysis: The model has low error in the top rows (0 and 1), which are dominated by Building and Vegetation. However, Row 3 — dominated by Road — still shows high error. This likely reflects geometric and viewpoint differences (camera position and scene layout) between the datasets.

| Synthia | Col 0 | Col 1 | Col 2 | Col 3 |
|:---:|:---:|:---:|:---:|:---:|
| Row 0 | Building (61.55%) (Err: 3.00%)<br>Sky (19.74%) (Err: 1.62%)<br>Vegetation (14.82%) (Err: 8.53%)<br>Pole (0.87%) (Err: 33.31%)<br>Sidewalk (0.85%) (Err: 29.24%) | Building (50.36%) (Err: 2.73%)<br>Sky (31.95%) (Err: 2.24%)<br>Vegetation (13.19%) (Err: 7.48%)<br>Sidewalk (1.11%) (Err: 19.95%)<br>Road (0.94%) (Err: 18.38%) | Building (50.42%) (Err: 2.68%)<br>Sky (32.78%) (Err: 2.98%)<br>Vegetation (12.67%) (Err: 9.04%)<br>Sidewalk (1.08%) (Err: 20.25%)<br>Pole (0.89%) (Err: 40.96%) | Building (62.42%) (Err: 2.61%)<br>Sky (20.29%) (Err: 3.41%)<br>Vegetation (14.01%) (Err: 6.54%)<br>Pole (0.98%) (Err: 28.63%)<br>Sidewalk (0.78%) (Err: 17.41%) |
| Row 1 | Building (49.21%) (Err: 3.05%)<br>Vegetation (17.56%) (Err: 6.92%)<br>Sidewalk (7.42%) (Err: 11.08%)<br>Road (7.40%) (Err: 10.05%)<br>Bus (5.50%) (Err: 5.36%) | Building (39.09%) (Err: 3.78%)<br>Vegetation (19.33%) (Err: 6.86%)<br>Sidewalk (10.42%) (Err: 13.02%)<br>Road (10.42%) (Err: 10.71%)<br>Person (6.25%) (Err: 19.26%) | Building (40.37%) (Err: 5.54%)<br>Vegetation (20.31%) (Err: 6.90%)<br>Sidewalk (11.23%) (Err: 13.52%)<br>Road (9.61%) (Err: 12.35%)<br>Person (6.30%) (Err: 22.60%) | Building (55.32%) (Err: 3.39%)<br>Vegetation (19.27%) (Err: 6.90%)<br>Sidewalk (7.96%) (Err: 11.89%)<br>Road (5.07%) (Err: 14.20%)<br>Person (4.60%) (Err: 23.09%) |
| Row 2 | Road (27.06%) (Err: 3.37%)<br>Sidewalk (26.79%) (Err: 3.51%)<br>Building (14.51%) (Err: 2.16%)<br>Car (9.22%) (Err: 3.18%)<br>Vegetation (8.77%) (Err: 6.29%) | Road (35.40%) (Err: 3.07%)<br>Sidewalk (31.34%) (Err: 3.38%)<br>Car (7.95%) (Err: 3.34%)<br>Person (7.68%) (Err: 8.65%)<br>Vegetation (7.19%) (Err: 6.12%) | Sidewalk (34.90%) (Err: 3.63%)<br>Road (34.11%) (Err: 3.31%)<br>Person (8.36%) (Err: 10.72%)<br>Car (6.48%) (Err: 3.67%)<br>Vegetation (5.63%) (Err: 6.38%) | Sidewalk (32.50%) (Err: 4.63%)<br>Road (22.48%) (Err: 4.62%)<br>Building (15.44%) (Err: 2.96%)<br>Person (9.17%) (Err: 12.25%)<br>Vegetation (7.93%) (Err: 9.01%) |
| Row 3 | Road (38.01%) (Err: 1.03%)<br>Sidewalk (35.71%) (Err: 1.36%)<br>Car (7.10%) (Err: 1.12%)<br>Building (6.40%) (Err: 3.90%)<br>Vegetation (4.46%) (Err: 10.35%) | Sidewalk (42.20%) (Err: 1.15%)<br>Road (41.26%) (Err: 0.75%)<br>Car (5.22%) (Err: 0.93%)<br>Person (3.96%) (Err: 4.25%)<br>Vegetation (2.59%) (Err: 8.43%) | Sidewalk (43.75%) (Err: 1.30%)<br>Road (39.90%) (Err: 1.00%)<br>Car (4.52%) (Err: 0.99%)<br>Person (4.16%) (Err: 6.24%)<br>Building (2.96%) (Err: 1.03%) | Sidewalk (40.35%) (Err: 1.82%)<br>Road (34.99%) (Err: 1.70%)<br>Building (6.83%) (Err: 0.87%)<br>Car (6.10%) (Err: 1.29%)<br>Person (4.77%) (Err: 8.77%) |

SYNTHIA analysis: Unlike Cityscapes, the bottom row shows much lower error for dominant classes such as Road and Sidewalk. The top rows are dominated by Building, Sky, and Vegetation, which also show low error.

### 4x4 Grid by Class: Error Distribution by Spatial Region (Filtered by Representation > 0.5%) (Top 5)

The following tables show the top 5 classes with the highest errors for each cell of the grid for Cityscapes and Synthia. We set a minimum representation threshold of 0.5% to filter noisy, extremely rare classes (e.g., very small counts of Person in distant grid cells).

| Cityscapes | Col 0 | Col 1 | Col 2 | Col 3 |
|:---:|:---:|:---:|:---:|:---:|
| Row 0 | Pole (1.71%) (Err: 29.03%)<br>Traffic sign (1.01%) (Err: 12.87%)<br>Vegetation (38.06%) (Err: 4.36%)<br>Building (51.12%) (Err: 3.81%)<br>Sky (6.72%) (Err: 0.88%) | Pole (1.09%) (Err: 42.56%)<br>Vegetation (40.08%) (Err: 4.37%)<br>Building (37.02%) (Err: 3.32%)<br>Sky (20.73%) (Err: 0.87%) | Pole (1.33%) (Err: 41.56%)<br>Traffic sign (1.00%) (Err: 12.11%)<br>Vegetation (40.22%) (Err: 4.05%)<br>Building (40.15%) (Err: 3.52%)<br>Sky (16.50%) (Err: 1.24%) | Fence (0.58%) (Err: 100.00%)<br>Pole (1.91%) (Err: 30.60%)<br>Traffic light (0.58%) (Err: 16.34%)<br>Traffic sign (2.34%) (Err: 14.18%)<br>Vegetation (34.43%) (Err: 3.91%) |
| Row 1 | Fence (2.58%) (Err: 90.59%)<br>Traffic sign (0.92%) (Err: 44.67%)<br>Rider (0.53%) (Err: 37.36%)<br>Wall (2.00%) (Err: 33.15%)<br>Pole (3.37%) (Err: 32.37%) | Fence (1.07%) (Err: 89.43%)<br>Pole (2.97%) (Err: 53.29%)<br>Traffic sign (1.00%) (Err: 51.00%)<br>Bicycle (1.28%) (Err: 36.88%)<br>Rider (0.84%) (Err: 34.45%) | Fence (1.25%) (Err: 93.92%)<br>Wall (1.13%) (Err: 53.54%)<br>Pole (3.34%) (Err: 52.26%)<br>Traffic sign (1.66%) (Err: 34.24%)<br>Bicycle (1.40%) (Err: 33.83%) | Fence (4.33%) (Err: 95.56%)<br>Wall (2.42%) (Err: 41.52%)<br>Traffic sign (0.97%) (Err: 34.48%)<br>Sidewalk (3.54%) (Err: 31.22%)<br>Bicycle (1.85%) (Err: 28.68%) |
| Row 2 | Fence (1.02%) (Err: 78.07%)<br>Bicycle (1.76%) (Err: 26.53%)<br>Vegetation (3.03%) (Err: 22.88%)<br>Pole (1.01%) (Err: 21.89%)<br>Building (2.74%) (Err: 21.79%) | Vegetation (0.92%) (Err: 36.29%)<br>Bicycle (0.56%) (Err: 31.95%)<br>Building (0.89%) (Err: 26.12%)<br>Sidewalk (5.02%) (Err: 16.04%)<br>Person (1.13%) (Err: 9.65%) | Bicycle (0.69%) (Err: 32.94%)<br>Vegetation (0.66%) (Err: 24.51%)<br>Building (0.79%) (Err: 15.10%)<br>Sidewalk (7.86%) (Err: 13.21%)<br>Road (84.05%) (Err: 9.23%) | Fence (1.10%) (Err: 79.40%)<br>Vegetation (3.03%) (Err: 28.83%)<br>Bicycle (1.72%) (Err: 25.63%)<br>Wall (0.90%) (Err: 25.61%)<br>Pole (1.59%) (Err: 14.94%) |
| Row 3 | Road (92.34%) (Err: 20.63%)<br>Car (1.82%) (Err: 9.74%)<br>Sidewalk (4.59%) (Err: 8.45%) | Road (99.43%) (Err: 23.80%)<br>Sidewalk (0.52%) (Err: 9.75%) | Road (99.44%) (Err: 23.46%) | Road (84.89%) (Err: 19.01%)<br>Car (1.65%) (Err: 11.61%)<br>Sidewalk (12.70%) (Err: 10.54%) |

Cityscapes analysis: In the top rows (0 and 1), the largest errors are concentrated on thin structures such as Pole and Traffic Sign, especially against complex backgrounds. Fence is also often missed in these rows. Overall, the model struggles most with small, low-support classes rather than with dominant background regions.


| Synthia | Col 0 | Col 1 | Col 2 | Col 3 |
|:---:|:---:|:---:|:---:|:---:|
| Row 0 | Pole (0.87%) (Err: 33.31%)<br>Sidewalk (0.85%) (Err: 29.24%)<br>Road (0.75%) (Err: 18.57%)<br>Bus (0.51%) (Err: 10.54%)<br>Vegetation (14.82%) (Err: 8.53%) | Pole (0.93%) (Err: 39.76%)<br>Sidewalk (1.11%) (Err: 19.95%)<br>Road (0.94%) (Err: 18.38%)<br>Vegetation (13.19%) (Err: 7.48%)<br>Building (50.36%) (Err: 2.73%) | Pole (0.89%) (Err: 40.96%)<br>Road (0.79%) (Err: 23.60%)<br>Sidewalk (1.08%) (Err: 20.25%)<br>Car (0.53%) (Err: 17.50%)<br>Vegetation (12.67%) (Err: 9.04%) | Pole (0.98%) (Err: 28.63%)<br>Sidewalk (0.78%) (Err: 17.41%)<br>Vegetation (14.01%) (Err: 6.54%)<br>Sky (20.29%) (Err: 3.41%)<br>Building (62.42%) (Err: 2.61%) |
| Row 1 | Pole (1.39%) (Err: 39.69%)<br>Person (3.67%) (Err: 18.44%)<br>Sidewalk (7.42%) (Err: 11.08%)<br>Road (7.40%) (Err: 10.05%)<br>Wall (0.77%) (Err: 9.44%) | Rider (0.64%) (Err: 52.62%)<br>Pole (1.62%) (Err: 48.56%)<br>Person (6.25%) (Err: 19.26%)<br>Sidewalk (10.42%) (Err: 13.02%)<br>Car (4.23%) (Err: 11.83%) | Rider (0.55%) (Err: 55.55%)<br>Pole (1.54%) (Err: 47.77%)<br>Person (6.30%) (Err: 22.60%)<br>Sidewalk (11.23%) (Err: 13.52%)<br>Car (3.68%) (Err: 13.18%) | Pole (1.41%) (Err: 40.29%)<br>Person (4.60%) (Err: 23.09%)<br>Road (5.07%) (Err: 14.20%)<br>Car (2.33%) (Err: 13.57%)<br>Sidewalk (7.96%) (Err: 11.89%) |
| Row 2 | Bicycle (0.50%) (Err: 41.51%)<br>Pole (0.76%) (Err: 18.36%)<br>Rider (1.17%) (Err: 14.69%)<br>Person (6.05%) (Err: 7.49%)<br>Vegetation (8.77%) (Err: 6.29%) | Pole (0.74%) (Err: 19.39%)<br>Rider (1.06%) (Err: 19.11%)<br>Motorcycle (0.72%) (Err: 15.65%)<br>Person (7.68%) (Err: 8.65%)<br>Fence (0.75%) (Err: 8.28%) | Pole (1.04%) (Err: 22.32%)<br>Rider (0.96%) (Err: 21.22%)<br>Person (8.36%) (Err: 10.72%)<br>Fence (1.06%) (Err: 8.61%)<br>Vegetation (5.63%) (Err: 6.38%) | Rider (0.94%) (Err: 24.53%)<br>Pole (1.14%) (Err: 23.30%)<br>Person (9.17%) (Err: 12.25%)<br>Fence (0.57%) (Err: 12.12%)<br>Vegetation (7.93%) (Err: 9.01%) |
| Row 3 | Rider (0.73%) (Err: 17.56%)<br>Vegetation (4.46%) (Err: 10.35%)<br>Person (3.99%) (Err: 4.29%)<br>Building (6.40%) (Err: 3.90%)<br>Sidewalk (35.71%) (Err: 1.36%) | Vegetation (2.59%) (Err: 8.43%)<br>Rider (0.51%) (Err: 7.69%)<br>Person (3.96%) (Err: 4.25%)<br>Building (2.08%) (Err: 2.44%)<br>Sidewalk (42.20%) (Err: 1.15%) | Pole (0.57%) (Err: 10.17%)<br>Vegetation (1.90%) (Err: 8.48%)<br>Person (4.16%) (Err: 6.24%)<br>Sidewalk (43.75%) (Err: 1.30%)<br>Building (2.96%) (Err: 1.03%) | Rider (0.68%) (Err: 15.89%)<br>Person (4.77%) (Err: 8.77%)<br>Vegetation (4.07%) (Err: 7.79%)<br>Bus (0.87%) (Err: 4.85%)<br>Sidewalk (40.35%) (Err: 1.82%) |

SYNTHIA analysis: In SYNTHIA, Fence appears less frequently and is generally easier for the model than in Cityscapes, likely because the class has a different semantic definition across datasets. As in Cityscapes, thin structures remain difficult and are often absorbed into nearby background classes, producing higher errors, especially in the top rows (0 and 1).


## Class-by-Class Comparison

The following sections show 4 sample images (2 from Cityscapes, 2 from SYNTHIA) and their corresponding semantic labels for each of the 16 classes (Terrain, Truck and Train classes are not present in SYNTHIA dataset). 

### Definitions:
- Representativity: How much of the dataset (or a specific image) is made up of a specific class. Total pixels of Class A / Total pixels of all classes.
- IoU: Area of Overlap / Area of Union
- Accuracy: The percentage of pixels belonging to a class that your model predicted correctly. Correctly predicted pixels of Class A / Total ground truth pixels of Class A
- Error: The direct opposite of Accuracy. Error pixels of Class A / Total ground truth pixels of Class A (or 1 - Accuracy)
<!-- - Average Representation: The average percentage of a class per image, rather than across the whole dataset pool. Sum of (Representation of Class A in Image 1, Image 2, etc.) / Total number of images
- Average Error: Sum of (Error Rate of Class A in Image 1, Image 2, etc.) / Total number of images -->

### 1. Road
| Metric | Cityscapes | SYNTHIA |
|---|---:|---:|
| Representativity | 38.14% | 18.97% |
| IoU | 82.15% | 94.39% |
| Accuracy | 84.95% | 96.65% |
| Error | 15.05% | 3.35% |
| Confused Classes<br>(Top 3) |  sidewalk (12.16%)<br>vegetation (1.50%)<br>car (0.56%)  | vegetation (0.84%)<br>sidewalk (0.80%)<br>person (0.68%) |

*Comment:* Road is the dominant class; Cityscapes shows notable error (often confused with sidewalk), while SYNTHIA predictions are very accurate.
<!-- | Average Representation | 37.71% | 19.05% |
| Average Error | 15.19% | 9.03% | -->

**Samples 1-2:**
| CS Image 1 | CS Image 2 | SYNTHIA Image 1 | SYNTHIA Image 2 |
|-----------|-----------|-----------|-----------|
| ![cs_road_1](assets/cityscapes_class_samples/road/sample_1_img.png) | ![cs_road_2](assets/cityscapes_class_samples/road/sample_2_img.png) | ![synthia_road_1](assets/synthia_subset_500_class_samples/road/synthia_sample_6_img.png) | ![synthia_road_2](assets/synthia_subset_500_class_samples/road/synthia_sample_2_img.png) |

| CS Label 1 | CS Label 2 | SYNTHIA Label 1 | SYNTHIA Label 2 |
|-----------|-----------|-----------|-----------|
| ![cs_road_1_label](assets/cityscapes_class_samples/road/sample_1_label.png) | ![cs_road_2_label](assets/cityscapes_class_samples/road/sample_2_label.png) | ![synthia_road_1_label](assets/synthia_subset_500_class_samples/road/synthia_sample_6_label.png) | ![synthia_road_2_label](assets/synthia_subset_500_class_samples/road/synthia_sample_2_label.png) |

<!-- **Samples 3-4:**
| CS Image 3 | CS Image 4 | SYNTHIA Image 3 | SYNTHIA Image 4 |
|-----------|-----------|-----------|-----------|
| ![cs_road_3](assets/cityscapes_class_samples/road/sample_3_img.png) | ![cs_road_4](assets/cityscapes_class_samples/road/sample_4_img.png) | ![synthia_road_3](assets/synthia_subset_500_class_samples/road/synthia_sample_3_img.png) | ![synthia_road_4](assets/synthia_subset_500_class_samples/road/synthia_sample_4_img.png) |

| CS Label 3 | CS Label 4 | SYNTHIA Label 3 | SYNTHIA Label 4 |
|-----------|-----------|-----------|-----------|
| ![cs_road_3_label](assets/cityscapes_class_samples/road/sample_3_label.png) | ![cs_road_4_label](assets/cityscapes_class_samples/road/sample_4_label.png) | ![synthia_road_3_label](assets/synthia_subset_500_class_samples/road/synthia_sample_3_label.png) | ![synthia_road_4_label](assets/synthia_subset_500_class_samples/road/synthia_sample_4_label.png) | -->

### 2. Sidewalk
| Metric | Cityscapes | SYNTHIA |
|---|---:|---:|
| Representativity | 5.47% | 20.21% |
| IoU | 43.10% | 92.69% |
| Accuracy | 84.19% | 96.15% |
| Error | 15.81% | 3.85% |
| Confused Classes<br>(Top 3) | road (13.04%)<br>vegetation (1.02%)<br>building (0.52%) | vegetation (1.35%)<br>person (1.17%)<br>road (0.41%) |

*Comment:* Sidewalk has lower support in Cityscapes and is frequently mistaken for road; SYNTHIA shows much lower error.
<!-- | Average Representation | 5.38% | 20.14% |
| Average Error | 21.52% | 5.56% | -->

**Samples 1-2:**
| CS Image 1 | CS Image 2 | SYNTHIA Image 1 | SYNTHIA Image 2 |
|-----------|-----------|-----------|----------|
| ![cs_sidewalk_1](assets/cityscapes_class_samples/sidewalk/sample_1_img.png) | ![cs_sidewalk_2](assets/cityscapes_class_samples/sidewalk/sample_2_img.png) | ![synthia_sidewalk_1](assets/synthia_subset_500_class_samples/sidewalk/synthia_sample_1_img.png) | ![synthia_sidewalk_2](assets/synthia_subset_500_class_samples/sidewalk/synthia_sample_2_img.png) |

| CS Label 1 | CS Label 2 | SYNTHIA Label 1 | SYNTHIA Label 2 |
|-----------|-----------|-----------|----------|
| ![cs_sidewalk_1_label](assets/cityscapes_class_samples/sidewalk/sample_1_label.png) | ![cs_sidewalk_2_label](assets/cityscapes_class_samples/sidewalk/sample_2_label.png) | ![synthia_sidewalk_1_label](assets/synthia_subset_500_class_samples/sidewalk/synthia_sample_1_label.png) | ![synthia_sidewalk_2_label](assets/synthia_subset_500_class_samples/sidewalk/synthia_sample_2_label.png) |

<!-- **Samples 3-4:**
| CS Image 3 | CS Image 4 | SYNTHIA Image 3 | SYNTHIA Image 4 |
|-----------|-----------|-----------|----------|
| ![cs_sidewalk_3](assets/cityscapes_class_samples/sidewalk/sample_3_img.png) | ![cs_sidewalk_4](assets/cityscapes_class_samples/sidewalk/sample_4_img.png) | ![synthia_sidewalk_3](assets/synthia_subset_500_class_samples/sidewalk/synthia_sample_3_img.png) | ![synthia_sidewalk_4](assets/synthia_subset_500_class_samples/sidewalk/synthia_sample_4_img.png) |

| CS Label 3 | CS Label 4 | SYNTHIA Label 3 | SYNTHIA Label 4 |
|-----------|-----------|-----------|----------|
| ![cs_sidewalk_3_label](assets/cityscapes_class_samples/sidewalk/sample_3_label.png) | ![cs_sidewalk_4_label](assets/cityscapes_class_samples/sidewalk/sample_4_label.png) | ![synthia_sidewalk_3_label](assets/synthia_subset_500_class_samples/sidewalk/synthia_sample_3_label.png) | ![synthia_sidewalk_4_label](assets/synthia_subset_500_class_samples/sidewalk/synthia_sample_4_label.png) | -->

### 3. Building
| Metric | Cityscapes | SYNTHIA |
|---|---:|---:|
| Representativity | 22.19% | 29.57% |
| IoU | 88.08% | 94.18% |
| Accuracy | 94.00% | 96.82% |
| Error | 6.00% | 3.18% |
| Confused Classes<br>(Top 3) | vegetation (2.32%)<br>pole (0.78%)<br>wall (0.74%) | vegetation (2.21%)<br>person (0.25%)<br>sidewalk (0.25%) |

*Comment:* Building is well recovered overall; remaining errors usually come from nearby vegetation or from small structures such as poles or walls.
<!-- | Average Representation | 22.61% | 29.47% | -->
<!-- | Average Error | 8.94% | 4.24% | -->

**Samples 1-2:**
| CS Image 1 | CS Image 2 | SYNTHIA Image 1 | SYNTHIA Image 2 |
|-----------|-----------|-----------|----------|
| ![cs_building_1](assets/cityscapes_class_samples/building/sample_1_img.png) | ![cs_building_2](assets/cityscapes_class_samples/building/sample_2_img.png) | ![synthia_building_1](assets/synthia_subset_500_class_samples/building/synthia_sample_1_img.png) | ![synthia_building_2](assets/synthia_subset_500_class_samples/building/synthia_sample_2_img.png) |

| CS Label 1 | CS Label 2 | SYNTHIA Label 1 | SYNTHIA Label 2 |
|-----------|-----------|-----------|----------|
| ![cs_building_1_label](assets/cityscapes_class_samples/building/sample_1_label.png) | ![cs_building_2_label](assets/cityscapes_class_samples/building/sample_2_label.png) | ![synthia_building_1_label](assets/synthia_subset_500_class_samples/building/synthia_sample_1_label.png) | ![synthia_building_2_label](assets/synthia_subset_500_class_samples/building/synthia_sample_2_label.png) |

<!-- **Samples 3-4:**
| CS Image 3 | CS Image 4 | SYNTHIA Image 3 | SYNTHIA Image 4 |
|-----------|-----------|-----------|----------|
| ![cs_building_3](assets/cityscapes_class_samples/building/sample_3_img.png) | ![cs_building_4](assets/cityscapes_class_samples/building/sample_4_img.png) | ![synthia_building_3](assets/synthia_subset_500_class_samples/building/synthia_sample_3_img.png) | ![synthia_building_4](assets/synthia_subset_500_class_samples/building/synthia_sample_4_img.png) |

| CS Label 3 | CS Label 4 | SYNTHIA Label 3 | SYNTHIA Label 4 |
|-----------|-----------|-----------|----------|
| ![cs_building_3_label](assets/cityscapes_class_samples/building/sample_3_label.png) | ![cs_building_4_label](assets/cityscapes_class_samples/building/sample_4_label.png) | ![synthia_building_3_label](assets/synthia_subset_500_class_samples/building/synthia_sample_3_label.png) | ![synthia_building_4_label](assets/synthia_subset_500_class_samples/building/synthia_sample_4_label.png) | -->

### 4. Wall
| Metric | Cityscapes | SYNTHIA |
|---|---:|---:|
| Representativity | 0.74% | 0.26% |
| IoU | 46.22% | 81.76% |
| Accuracy | 66.13% | 88.04% |
| Error | 33.87% | 11.96% |
| Confused Classes<br>(Top 3) | building (15.92%)<br>sidewalk (6.99%)<br>vegetation (5.76%) | building (3.53%)<br>sidewalk (3.22%)<br>vegetation (2.53%) |

*Comment:* Wall is rare and error-prone in Cityscapes, often labeled as building or sidewalk; SYNTHIA shows fewer confusions.
<!-- | Average Representation | 0.82% | 0.25% |
| Average Error | 27.43% | 20.78% | -->

**Samples 1-2:**
| CS Image 1 | CS Image 2 | SYNTHIA Image 1 | SYNTHIA Image 2 |
|-----------|-----------|-----------|----------|
| ![cs_wall_1](assets/cityscapes_class_samples/wall/sample_1_img.png) | ![cs_wall_2](assets/cityscapes_class_samples/wall/sample_2_img.png) | ![synthia_wall_1](assets/synthia_subset_500_class_samples/wall/synthia_sample_1_img.png) | ![synthia_wall_2](assets/synthia_subset_500_class_samples/wall/synthia_sample_2_img.png) |

| CS Label 1 | CS Label 2 | SYNTHIA Label 1 | SYNTHIA Label 2 |
|-----------|-----------|-----------|----------|
| ![cs_wall_1_label](assets/cityscapes_class_samples/wall/sample_1_label.png) | ![cs_wall_2_label](assets/cityscapes_class_samples/wall/sample_2_label.png) | ![synthia_wall_1_label](assets/synthia_subset_500_class_samples/wall/synthia_sample_1_label.png) | ![synthia_wall_2_label](assets/synthia_subset_500_class_samples/wall/synthia_sample_2_label.png) |

<!-- **Samples 3-4:**
| CS Image 3 | CS Image 4 | SYNTHIA Image 3 | SYNTHIA Image 4 |
|-----------|-----------|-----------|----------|
| ![cs_wall_3](assets/cityscapes_class_samples/wall/sample_3_img.png) | ![cs_wall_4](assets/cityscapes_class_samples/wall/sample_4_img.png) | ![synthia_wall_3](assets/synthia_subset_500_class_samples/wall/synthia_sample_3_img.png) | ![synthia_wall_4](assets/synthia_subset_500_class_samples/wall/synthia_sample_4_img.png) |

| CS Label 3 | CS Label 4 | SYNTHIA Label 3 | SYNTHIA Label 4 |
|-----------|-----------|-----------|----------|
| ![cs_wall_3_label](assets/cityscapes_class_samples/wall/sample_3_label.png) | ![cs_wall_4_label](assets/cityscapes_class_samples/wall/sample_4_label.png) | ![synthia_wall_3_label](assets/synthia_subset_500_class_samples/wall/synthia_sample_3_label.png) | ![synthia_wall_4_label](assets/synthia_subset_500_class_samples/wall/synthia_sample_4_label.png) | -->

### 5. Fence

This class is completely dissimilar in the semantic meaning in cityscapes and synthia, causing that the model completely misses in the target validation.

| Metric | Cityscapes | SYNTHIA |
|---|---:|---:|
| Representativity | 0.83% | 0.31% |
| IoU | 8.47% | 77.54% |
| Accuracy | 9.76% | 86.67% |
| Error | 90.24% | 13.33% |
| Confused Classes<br>(Top 3) | building (39.48%)<br>vegetation (17.76%)<br>wall (13.14%) | road (6.10%)<br>sidewalk (1.88%)<br>person (1.60%) |

*Comment:* Fence semantics differ strongly between datasets; Cityscapes fences are often predicted as building/vegetation, while SYNTHIA confuses fence with road/sidewalk.
<!-- | Average Representation | 0.84% | 0.32% |
| Average Error | 35.42% | 44.81% | -->

**Samples 1-2:**
| CS Image 1 | CS Image 2 | SYNTHIA Image 1 | SYNTHIA Image 2 |
|-----------|-----------|-----------|----------|
| ![cs_fence_1](assets/cityscapes_class_samples/fence/sample_1_img.png) | ![cs_fence_2](assets/cityscapes_class_samples/fence/sample_2_img.png) | ![synthia_fence_1](assets/synthia_subset_500_class_samples/fence/synthia_sample_6_img.png) | ![synthia_fence_2](assets/synthia_subset_500_class_samples/fence/synthia_sample_2_img.png) |

| CS Label 1 | CS Label 2 | SYNTHIA Label 1 | SYNTHIA Label 2 |
|-----------|-----------|-----------|----------|
| ![cs_fence_1_label](assets/cityscapes_class_samples/fence/sample_1_label.png) | ![cs_fence_2_label](assets/cityscapes_class_samples/fence/sample_2_label.png) | ![synthia_fence_1_label](assets/synthia_subset_500_class_samples/fence/synthia_sample_6_label.png) | ![synthia_fence_2_label](assets/synthia_subset_500_class_samples/fence/synthia_sample_2_label.png) |

<!-- **Samples 3-4:**
| CS Image 3 | CS Image 4 | SYNTHIA Image 3 | SYNTHIA Image 4 |
|-----------|-----------|-----------|----------|
| ![cs_fence_3](assets/cityscapes_class_samples/fence/sample_3_img.png) | ![cs_fence_4](assets/cityscapes_class_samples/fence/sample_4_img.png) | ![synthia_fence_3](assets/synthia_subset_500_class_samples/fence/synthia_sample_3_img.png) | ![synthia_fence_4](assets/synthia_subset_500_class_samples/fence/synthia_sample_4_img.png) |

| CS Label 3 | CS Label 4 | SYNTHIA Label 3 | SYNTHIA Label 4 |
|-----------|-----------|-----------|----------|
| ![cs_fence_3_label](assets/cityscapes_class_samples/fence/sample_3_label.png) | ![cs_fence_4_label](assets/cityscapes_class_samples/fence/sample_4_label.png) | ![synthia_fence_3_label](assets/synthia_subset_500_class_samples/fence/synthia_sample_3_label.png) | ![synthia_fence_4_label](assets/synthia_subset_500_class_samples/fence/synthia_sample_4_label.png) | -->

### 6. Pole
| Metric | Cityscapes | SYNTHIA |
|---|---:|---:|
| Representativity | 1.50% | 0.94% |
| IoU | 50.95% | 55.29% |
| Accuracy | 63.80% | 66.90% |
| Error | 36.20% | 33.10% |
| Confused Classes<br>(Top 3) | building (14.86%)<br>vegetation (9.33%)<br>sidewalk (2.15%) | building (14.10%)<br>sidewalk (5.40%)<br>vegetation (5.04%) |

*Comment:* Pole is a thin, low-support class with high error; it is commonly absorbed into building or vegetation labels in both datasets.
<!-- | Average Representation | 1.52% | 0.94% |
| Average Error | 42.37% | 45.41% | -->

**Samples 1-2:**
| CS Image 1 | CS Image 2 | SYNTHIA Image 1 | SYNTHIA Image 2 |
|-----------|-----------|-----------|----------|
| ![cs_pole_1](assets/cityscapes_class_samples/pole/sample_1_img.png) | ![cs_pole_2](assets/cityscapes_class_samples/pole/sample_2_img.png) | ![synthia_pole_1](assets/synthia_subset_500_class_samples/pole/synthia_sample_1_img.png) | ![synthia_pole_2](assets/synthia_subset_500_class_samples/pole/synthia_sample_2_img.png) |

| CS Label 1 | CS Label 2 | SYNTHIA Label 1 | SYNTHIA Label 2 |
|-----------|-----------|-----------|----------|
| ![cs_pole_1_label](assets/cityscapes_class_samples/pole/sample_1_label.png) | ![cs_pole_2_label](assets/cityscapes_class_samples/pole/sample_2_label.png) | ![synthia_pole_1_label](assets/synthia_subset_500_class_samples/pole/synthia_sample_1_label.png) | ![synthia_pole_2_label](assets/synthia_subset_500_class_samples/pole/synthia_sample_2_label.png) |

<!-- **Samples 3-4:**
| CS Image 3 | CS Image 4 | SYNTHIA Image 3 | SYNTHIA Image 4 |
|-----------|-----------|-----------|----------|
| ![cs_pole_3](assets/cityscapes_class_samples/pole/sample_3_img.png) | ![cs_pole_4](assets/cityscapes_class_samples/pole/sample_4_img.png) | ![synthia_pole_3](assets/synthia_subset_500_class_samples/pole/synthia_sample_3_img.png) | ![synthia_pole_4](assets/synthia_subset_500_class_samples/pole/synthia_sample_4_img.png) |

| CS Label 3 | CS Label 4 | SYNTHIA Label 3 | SYNTHIA Label 4 |
|-----------|-----------|-----------|----------|
| ![cs_pole_3_label](assets/cityscapes_class_samples/pole/sample_3_label.png) | ![cs_pole_4_label](assets/cityscapes_class_samples/pole/sample_4_label.png) | ![synthia_pole_3_label](assets/synthia_subset_500_class_samples/pole/synthia_sample_3_label.png) | ![synthia_pole_4_label](assets/synthia_subset_500_class_samples/pole/synthia_sample_4_label.png) | -->

### 7. Traffic Light
| Metric | Cityscapes | SYNTHIA |
|---|---:|---:|
| Representativity | 0.20% | 0.04% |
| IoU | 54.40% | 56.10% |
| Accuracy | 65.92% | 60.87% |
| Error | 34.08% | 39.13% |
| Confused Classes<br>(Top 3) | vegetation (12.37%)<br>building (11.91%)<br>traffic sign (4.53%) | building (20.98%)<br>vegetation (7.60%)<br>pole (2.99%) |

*Comment:* Traffic lights are scarce and often confused with vegetation or nearby buildings in Cityscapes; SYNTHIA mainly mislabels them as building.
<!-- | Average Representation | 0.20% | 0.04% |
| Average Error | 35.78% | 55.62% | -->

**Samples 1-2:**
| CS Image 1 | CS Image 2 | SYNTHIA Image 1 | SYNTHIA Image 2 |
|-----------|-----------|-----------|----------|
| ![cs_tl_1](assets/cityscapes_class_samples/traffic%20light/sample_1_img.png) | ![cs_tl_2](assets/cityscapes_class_samples/traffic%20light/sample_2_img.png) | ![synthia_tl_1](assets/synthia_subset_500_class_samples/traffic%20light/synthia_sample_1_img.png) | ![synthia_tl_2](assets/synthia_subset_500_class_samples/traffic%20light/synthia_sample_6_img.png) |

| CS Label 1 | CS Label 2 | SYNTHIA Label 1 | SYNTHIA Label 2 |
|-----------|-----------|-----------|----------|
| ![cs_tl_1_label](assets/cityscapes_class_samples/traffic%20light/sample_1_label.png) | ![cs_tl_2_label](assets/cityscapes_class_samples/traffic%20light/sample_2_label.png) | ![synthia_tl_1_label](assets/synthia_subset_500_class_samples/traffic%20light/synthia_sample_1_label.png) | ![synthia_tl_2_label](assets/synthia_subset_500_class_samples/traffic%20light/synthia_sample_6_label.png) |

<!-- **Samples 3-4:**
| CS Image 3 | CS Image 4 | SYNTHIA Image 3 | SYNTHIA Image 4 |
|-----------|-----------|-----------|----------|
| ![cs_tl_3](assets/cityscapes_class_samples/traffic%20light/sample_3_img.png) | ![cs_tl_4](assets/cityscapes_class_samples/traffic%20light/sample_4_img.png) | ![synthia_tl_3](assets/synthia_subset_500_class_samples/traffic%20light/synthia_sample_3_img.png) | ![synthia_tl_4](assets/synthia_subset_500_class_samples/traffic%20light/synthia_sample_4_img.png) |

| CS Label 3 | CS Label 4 | SYNTHIA Label 3 | SYNTHIA Label 4 |
|-----------|-----------|-----------|----------|
| ![cs_tl_3_label](assets/cityscapes_class_samples/traffic%20light/sample_3_label.png) | ![cs_tl_4_label](assets/cityscapes_class_samples/traffic%20light/sample_4_label.png) | ![synthia_tl_3_label](assets/synthia_subset_500_class_samples/traffic%20light/synthia_sample_3_label.png) | ![synthia_tl_4_label](assets/synthia_subset_500_class_samples/traffic%20light/synthia_sample_4_label.png) | -->

### 8. Traffic Sign
| Metric | Cityscapes | SYNTHIA |
|---|---:|---:|
| Representativity | 0.68% | 0.09% |
| IoU | 53.28% | 57.78% |
| Accuracy | 68.61% | 63.32% |
| Error | 31.39% | 36.68% |
| Confused Classes<br>(Top 3) | fence (13.26%)<br>building (10.38%)<br>vegetation (3.49%) | building (11.87%)<br>person (6.41%)<br>vegetation (5.78%) |

*Comment:* Traffic signs are small and often merged into fence or building predictions; SYNTHIA shows notable confusion with person and building.
<!-- | Average Representation | 0.68% | 0.09% |
| Average Error | 29.68% | 67.80% | -->

**Samples 1-2:**
| CS Image 1 | CS Image 2 | SYNTHIA Image 1 | SYNTHIA Image 2 |
|-----------|-----------|-----------|----------|
| ![cs_ts_1](assets/cityscapes_class_samples/traffic%20sign/sample_1_img.png) | ![cs_ts_2](assets/cityscapes_class_samples/traffic%20sign/sample_2_img.png) | ![synthia_ts_1](assets/synthia_subset_500_class_samples/traffic%20sign/synthia_sample_1_img.png) | ![synthia_ts_2](assets/synthia_subset_500_class_samples/traffic%20sign/synthia_sample_2_img.png) |

| CS Label 1 | CS Label 2 | SYNTHIA Label 1 | SYNTHIA Label 2 |
|-----------|-----------|-----------|----------|
| ![cs_ts_1_label](assets/cityscapes_class_samples/traffic%20sign/sample_1_label.png) | ![cs_ts_2_label](assets/cityscapes_class_samples/traffic%20sign/sample_2_label.png) | ![synthia_ts_1_label](assets/synthia_subset_500_class_samples/traffic%20sign/synthia_sample_1_label.png) | ![synthia_ts_2_label](assets/synthia_subset_500_class_samples/traffic%20sign/synthia_sample_2_label.png) |

<!-- **Samples 3-4:**
| CS Image 3 | CS Image 4 | SYNTHIA Image 3 | SYNTHIA Image 4 |
|-----------|-----------|-----------|----------|
| ![cs_ts_3](assets/cityscapes_class_samples/traffic%20sign/sample_3_img.png) | ![cs_ts_4](assets/cityscapes_class_samples/traffic%20sign/sample_4_img.png) | ![synthia_ts_3](assets/synthia_subset_500_class_samples/traffic%20sign/synthia_sample_3_img.png) | ![synthia_ts_4](assets/synthia_subset_500_class_samples/traffic%20sign/synthia_sample_4_img.png) |

| CS Label 3 | CS Label 4 | SYNTHIA Label 3 | SYNTHIA Label 4 |
|-----------|-----------|-----------|----------|
| ![cs_ts_3_label](assets/cityscapes_class_samples/traffic%20sign/sample_3_label.png) | ![cs_ts_4_label](assets/cityscapes_class_samples/traffic%20sign/sample_4_label.png) | ![synthia_ts_3_label](assets/synthia_subset_500_class_samples/traffic%20sign/synthia_sample_3_label.png) | ![synthia_ts_4_label](assets/synthia_subset_500_class_samples/traffic%20sign/synthia_sample_4_label.png) | -->

### 9. Vegetation
| Metric | Cityscapes | SYNTHIA |
|---|---:|---:|
| Representativity | 17.53% | 10.94% |
| IoU | 84.55% | 81.68% |
| Accuracy | 94.24% | 92.62% |
| Error | 5.76% | 7.38% |
| Confused Classes<br>(Top 3) | building (2.13%)<br>sky (1.37%)<br>road (0.82%) | building (3.37%)<br>sidewalk (1.48%)<br>road (0.73%) |

*Comment:* Vegetation is reliably predicted in both datasets, with minor confusions into building or sky for thin or distant foliage.
<!-- | Average Representation | 17.63% | 11.00% |
| Average Error | 7.20% | 11.45% | -->

**Samples 1-2:**
| CS Image 1 | CS Image 2 | SYNTHIA Image 1 | SYNTHIA Image 2 |
|-----------|-----------|-----------|----------|
| ![cs_veg_1](assets/cityscapes_class_samples/vegetation/sample_1_img.png) | ![cs_veg_2](assets/cityscapes_class_samples/vegetation/sample_2_img.png) | ![synthia_veg_1](assets/synthia_subset_500_class_samples/vegetation/synthia_sample_1_img.png) | ![synthia_veg_2](assets/synthia_subset_500_class_samples/vegetation/synthia_sample_2_img.png) |

| CS Label 1 | CS Label 2 | SYNTHIA Label 1 | SYNTHIA Label 2 |
|-----------|-----------|-----------|----------|
| ![cs_veg_1_label](assets/cityscapes_class_samples/vegetation/sample_1_label.png) | ![cs_veg_2_label](assets/cityscapes_class_samples/vegetation/sample_2_label.png) | ![synthia_veg_1_label](assets/synthia_subset_500_class_samples/vegetation/synthia_sample_1_label.png) | ![synthia_veg_2_label](assets/synthia_subset_500_class_samples/vegetation/synthia_sample_2_label.png) |

<!-- **Samples 3-4:**
| CS Image 3 | CS Image 4 | SYNTHIA Image 3 | SYNTHIA Image 4 |
|-----------|-----------|-----------|----------|
| ![cs_veg_3](assets/cityscapes_class_samples/vegetation/sample_3_img.png) | ![cs_veg_4](assets/cityscapes_class_samples/vegetation/sample_4_img.png) | ![synthia_veg_3](assets/synthia_subset_500_class_samples/vegetation/synthia_sample_3_img.png) | ![synthia_veg_4](assets/synthia_subset_500_class_samples/vegetation/synthia_sample_4_img.png) |

| CS Label 3 | CS Label 4 | SYNTHIA Label 3 | SYNTHIA Label 4 |
|-----------|-----------|-----------|----------|
| ![cs_veg_3_label](assets/cityscapes_class_samples/vegetation/sample_3_label.png) | ![cs_veg_4_label](assets/cityscapes_class_samples/vegetation/sample_4_label.png) | ![synthia_veg_3_label](assets/synthia_subset_500_class_samples/vegetation/synthia_sample_3_label.png) | ![synthia_veg_4_label](assets/synthia_subset_500_class_samples/vegetation/synthia_sample_4_label.png) | -->

### 11. Sky
| Metric | Cityscapes | SYNTHIA |
|---|---:|---:|
| Representativity | 3.39% | 7.28% |
| IoU | 87.41% | 95.57% |
| Accuracy | 98.86% | 97.22% |
| Error | 1.14% | 2.78% |
| Confused Classes<br>(Top 3) | vegetation (0.55%)<br>building (0.40%)<br>pole (0.14%) | vegetation (1.73%)<br>building (0.93%)<br>pole (0.12%) |

*Comment:* Sky has very low error overall.
<!-- | Average Representation | 3.34% | 7.29% |
| Average Error | 4.40% | 6.77% | -->

**Samples 1-2:**
| CS Image 1 | CS Image 2 | SYNTHIA Image 1 | SYNTHIA Image 2 |
|-----------|-----------|-----------|----------|
| ![cs_sky_1](assets/cityscapes_class_samples/sky/sample_1_img.png) | ![cs_sky_2](assets/cityscapes_class_samples/sky/sample_2_img.png) | ![synthia_sky_1](assets/synthia_subset_500_class_samples/sky/synthia_sample_1_img.png) | ![synthia_sky_2](assets/synthia_subset_500_class_samples/sky/synthia_sample_2_img.png) |

| CS Label 1 | CS Label 2 | SYNTHIA Label 1 | SYNTHIA Label 2 |
|-----------|-----------|-----------|----------|
| ![cs_sky_1_label](assets/cityscapes_class_samples/sky/sample_1_label.png) | ![cs_sky_2_label](assets/cityscapes_class_samples/sky/sample_2_label.png) | ![synthia_sky_1_label](assets/synthia_subset_500_class_samples/sky/synthia_sample_1_label.png) | ![synthia_sky_2_label](assets/synthia_subset_500_class_samples/sky/synthia_sample_2_label.png) |

<!-- **Samples 3-4:**
| CS Image 3 | CS Image 4 | SYNTHIA Image 3 | SYNTHIA Image 4 |
|-----------|-----------|-----------|----------|
| ![cs_sky_3](assets/cityscapes_class_samples/sky/sample_3_img.png) | ![cs_sky_4](assets/cityscapes_class_samples/sky/sample_4_img.png) | ![synthia_sky_3](assets/synthia_subset_500_class_samples/sky/synthia_sample_3_img.png) | ![synthia_sky_4](assets/synthia_subset_500_class_samples/sky/synthia_sample_10_img.png) |

| CS Label 3 | CS Label 4 | SYNTHIA Label 3 | SYNTHIA Label 4 |
|-----------|-----------|-----------|----------|
| ![cs_sky_3_label](assets/cityscapes_class_samples/sky/sample_3_label.png) | ![cs_sky_4_label](assets/cityscapes_class_samples/sky/sample_4_label.png) | ![synthia_sky_3_label](assets/synthia_subset_500_class_samples/sky/synthia_sample_3_label.png) | ![synthia_sky_4_label](assets/synthia_subset_500_class_samples/sky/synthia_sample_10_label.png) | -->

### 12. Person
| Metric | Cityscapes | SYNTHIA |
|---|---:|---:|
| Representativity | 1.31% | 4.33% |
| IoU | 72.75% | 75.83% |
| Accuracy | 88.38% | 86.97% |
| Error | 11.62% | 13.03% |
| Confused Classes<br>(Top 3) | building (2.95%)<br>rider (1.89%)<br>car (1.56%) | sidewalk (5.11%)<br>road (2.30%)<br>building (2.15%) |

*Comment:* Person detection is moderate, showing a small gap between the datasets; Cityscapes confuses people with building or rider, while SYNTHIA tends to label them as sidewalk or road.
<!-- | Average Representation | 1.32% | 4.32% |
| Average Error | 27.38% | 19.43% | -->

**Samples 1-2:**
| CS Image 1 | CS Image 2 | SYNTHIA Image 1 | SYNTHIA Image 2 |
|-----------|-----------|-----------|----------|
| ![cs_person_1](assets/cityscapes_class_samples/person/sample_1_img.png) | ![cs_person_2](assets/cityscapes_class_samples/person/sample_2_img.png) | ![synthia_person_1](assets/synthia_subset_500_class_samples/person/synthia_sample_1_img.png) | ![synthia_person_2](assets/synthia_subset_500_class_samples/person/synthia_sample_2_img.png) |

| CS Label 1 | CS Label 2 | SYNTHIA Label 1 | SYNTHIA Label 2 |
|-----------|-----------|-----------|----------|
| ![cs_person_1_label](assets/cityscapes_class_samples/person/sample_1_label.png) | ![cs_person_2_label](assets/cityscapes_class_samples/person/sample_2_label.png) | ![synthia_person_1_label](assets/synthia_subset_500_class_samples/person/synthia_sample_1_label.png) | ![synthia_person_2_label](assets/synthia_subset_500_class_samples/person/synthia_sample_2_label.png) |

<!-- **Samples 3-4:**
| CS Image 3 | CS Image 4 | SYNTHIA Image 3 | SYNTHIA Image 4 |
|-----------|-----------|-----------|----------|
| ![cs_person_3](assets/cityscapes_class_samples/person/sample_3_img.png) | ![cs_person_4](assets/cityscapes_class_samples/person/sample_4_img.png) | ![synthia_person_3](assets/synthia_subset_500_class_samples/person/synthia_sample_3_img.png) | ![synthia_person_4](assets/synthia_subset_500_class_samples/person/synthia_sample_4_img.png) |

| CS Label 3 | CS Label 4 | SYNTHIA Label 3 | SYNTHIA Label 4 |
|-----------|-----------|-----------|----------|
| ![cs_person_3_label](assets/cityscapes_class_samples/person/sample_3_label.png) | ![cs_person_4_label](assets/cityscapes_class_samples/person/sample_4_label.png) | ![synthia_person_3_label](assets/synthia_subset_500_class_samples/person/synthia_sample_3_label.png) | ![synthia_person_4_label](assets/synthia_subset_500_class_samples/person/synthia_sample_4_label.png) | -->

### 13. Rider
| Metric | Cityscapes | SYNTHIA |
|---|---:|---:|
| Representativity | 0.22% | 0.52% |
| IoU | 46.60% | 63.49% |
| Accuracy | 65.93% | 73.16% |
| Error | 34.07% | 26.84% |
| Confused Classes<br>(Top 3) | person (18.84%)<br>bicycle (5.85%)<br>car (2.52%) | person (9.33%)<br>road (3.90%)<br>sidewalk (2.96%) |

*Comment:* Rider is often mistaken for person or bicycle in Cityscapes; SYNTHIA still confuses riders with person and road.
<!-- | Average Representation | 0.21% | 0.52% |
| Average Error | 27.20% | 49.27% | -->

**Samples 1-2:**
| CS Image 1 | CS Image 2 | SYNTHIA Image 1 | SYNTHIA Image 2 |
|-----------|-----------|-----------|----------|
| ![cs_rider_1](assets/cityscapes_class_samples/rider/sample_1_img.png) | ![cs_rider_2](assets/cityscapes_class_samples/rider/sample_2_img.png) | ![synthia_rider_1](assets/synthia_subset_500_class_samples/rider/synthia_sample_1_img.png) | ![synthia_rider_2](assets/synthia_subset_500_class_samples/rider/synthia_sample_2_img.png) |

| CS Label 1 | CS Label 2 | SYNTHIA Label 1 | SYNTHIA Label 2 |
|-----------|-----------|-----------|----------|
| ![cs_rider_1_label](assets/cityscapes_class_samples/rider/sample_1_label.png) | ![cs_rider_2_label](assets/cityscapes_class_samples/rider/sample_2_label.png) | ![synthia_rider_1_label](assets/synthia_subset_500_class_samples/rider/synthia_sample_1_label.png) | ![synthia_rider_2_label](assets/synthia_subset_500_class_samples/rider/synthia_sample_2_label.png) |

<!-- **Samples 3-4:**
| CS Image 3 | CS Image 4 | SYNTHIA Image 3 | SYNTHIA Image 4 |
|-----------|-----------|-----------|----------|
| ![cs_rider_3](assets/cityscapes_class_samples/rider/sample_3_img.png) | ![cs_rider_4](assets/cityscapes_class_samples/rider/sample_4_img.png) | ![synthia_rider_3](assets/synthia_subset_500_class_samples/rider/synthia_sample_3_img.png) | ![synthia_rider_4](assets/synthia_subset_500_class_samples/rider/synthia_sample_4_img.png) |

| CS Label 3 | CS Label 4 | SYNTHIA Label 3 | SYNTHIA Label 4 |
|-----------|-----------|-----------|----------|
| ![cs_rider_3_label](assets/cityscapes_class_samples/rider/sample_3_label.png) | ![cs_rider_4_label](assets/cityscapes_class_samples/rider/sample_4_label.png) | ![synthia_rider_3_label](assets/synthia_subset_500_class_samples/rider/synthia_sample_3_label.png) | ![synthia_rider_4_label](assets/synthia_subset_500_class_samples/rider/synthia_sample_4_label.png) | -->

### 14. Car
| Metric | Cityscapes | SYNTHIA |
|---|---:|---:|
| Representativity | 6.60% | 4.29% |
| IoU | 85.87% | 90.78% |
| Accuracy | 95.53% | 95.18% |
| Error | 4.47% | 4.82% |
| Confused Classes<br>(Top 3) | road (1.73%)<br>building (0.70%)<br>vegetation (0.58%) | road (1.27%)<br>vegetation (1.27%)<br>person (0.76%) |

*Comment:* Car predictions are strong in both datasets; most errors are small and come from road or nearby vegetation.
<!-- | Average Representation | 6.56% | 4.30% |
| Average Error | 7.65% | 18.87% | -->

**Samples 1-2:**
| CS Image 1 | CS Image 2 | SYNTHIA Image 1 | SYNTHIA Image 2 |
|-----------|-----------|-----------|----------|
| ![cs_car_1](assets/cityscapes_class_samples/car/sample_1_img.png) | ![cs_car_2](assets/cityscapes_class_samples/car/sample_2_img.png) | ![synthia_car_1](assets/synthia_subset_500_class_samples/car/synthia_sample_8_img.png) | ![synthia_car_2](assets/synthia_subset_500_class_samples/car/synthia_sample_2_img.png) |

| CS Label 1 | CS Label 2 | SYNTHIA Label 1 | SYNTHIA Label 2 |
|-----------|-----------|-----------|----------|
| ![cs_car_1_label](assets/cityscapes_class_samples/car/sample_1_label.png) | ![cs_car_2_label](assets/cityscapes_class_samples/car/sample_2_label.png) | ![synthia_car_1_label](assets/synthia_subset_500_class_samples/car/synthia_sample_8_label.png) | ![synthia_car_2_label](assets/synthia_subset_500_class_samples/car/synthia_sample_2_label.png) |

<!-- **Samples 3-4:**
| CS Image 3 | CS Image 4 | SYNTHIA Image 3 | SYNTHIA Image 4 |
|-----------|-----------|-----------|----------|
| ![cs_car_3](assets/cityscapes_class_samples/car/sample_3_img.png) | ![cs_car_4](assets/cityscapes_class_samples/car/sample_4_img.png) | ![synthia_car_3](assets/synthia_subset_500_class_samples/car/synthia_sample_3_img.png) | ![synthia_car_4](assets/synthia_subset_500_class_samples/car/synthia_sample_5_img.png) |

| CS Label 3 | CS Label 4 | SYNTHIA Label 3 | SYNTHIA Label 4 |
|-----------|-----------|-----------|----------|
| ![cs_car_3_label](assets/cityscapes_class_samples/car/sample_3_label.png) | ![cs_car_4_label](assets/cityscapes_class_samples/car/sample_4_label.png) | ![synthia_car_3_label](assets/synthia_subset_500_class_samples/car/synthia_sample_3_label.png) | ![synthia_car_4_label](assets/synthia_subset_500_class_samples/car/synthia_sample_5_label.png) | -->

### 16. Bus
| Metric | Cityscapes | SYNTHIA |
|---|---:|---:|
| Representativity | 0.39% | 1.80% |
| IoU | 60.32% | 91.63% |
| Accuracy | 84.48% | 94.55% |
| Error | 15.52% | 5.45% |
| Confused Classes<br>(Top 3) | car (7.38%)<br>vegetation (2.43%)<br>building (2.27%) | vegetation (1.85%)<br>building (1.13%)<br>car (0.80%) |

*Comment:* Bus is low-support; errors often bleed into car or vegetation labels but remain moderate in SYNTHIA.
<!-- | Average Representation | 0.39% | 1.82% |
| Average Error | 5.49% | 21.84% | -->

**Samples 1-2:**
| CS Image 1 | CS Image 2 | SYNTHIA Image 1 | SYNTHIA Image 2 |
|-----------|-----------|-----------|----------|
| ![cs_bus_1](assets/cityscapes_class_samples/bus/sample_1_img.png) | ![cs_bus_2](assets/cityscapes_class_samples/bus/sample_2_img.png) | ![synthia_bus_1](assets/synthia_subset_500_class_samples/bus/synthia_sample_1_img.png) | ![synthia_bus_2](assets/synthia_subset_500_class_samples/bus/synthia_sample_6_img.png) |

| CS Label 1 | CS Label 2 | SYNTHIA Label 1 | SYNTHIA Label 2 |
|-----------|-----------|-----------|----------|
| ![cs_bus_1_label](assets/cityscapes_class_samples/bus/sample_1_label.png) | ![cs_bus_2_label](assets/cityscapes_class_samples/bus/sample_2_label.png) | ![synthia_bus_1_label](assets/synthia_subset_500_class_samples/bus/synthia_sample_1_label.png) | ![synthia_bus_2_label](assets/synthia_subset_500_class_samples/bus/synthia_sample_6_label.png) |

<!-- **Samples 3-4:**
| CS Image 3 | CS Image 4 | SYNTHIA Image 3 | SYNTHIA Image 4 |
|-----------|-----------|-----------|----------|
| ![cs_bus_3](assets/cityscapes_class_samples/bus/sample_3_img.png) | ![cs_bus_4](assets/cityscapes_class_samples/bus/sample_4_img.png) | ![synthia_bus_3](assets/synthia_subset_500_class_samples/bus/synthia_sample_3_img.png) | ![synthia_bus_4](assets/synthia_subset_500_class_samples/bus/synthia_sample_9_img.png) |

| CS Label 3 | CS Label 4 | SYNTHIA Label 3 | SYNTHIA Label 4 |
|-----------|-----------|-----------|----------|
| ![cs_bus_3_label](assets/cityscapes_class_samples/bus/sample_3_label.png) | ![cs_bus_4_label](assets/cityscapes_class_samples/bus/sample_4_label.png) | ![synthia_bus_3_label](assets/synthia_subset_500_class_samples/bus/synthia_sample_3_label.png) | ![synthia_bus_4_label](assets/synthia_subset_500_class_samples/bus/synthia_sample_9_label.png) | -->

### 18. Motorcycle
| Metric | Cityscapes | SYNTHIA |
|---|---:|---:|
| Representativity | 0.08% | 0.21% |
| IoU | 53.26% | 69.10% |
| Accuracy | 61.02% | 77.72% |
| Error | 38.98% | 22.28% |
| Confused Classes<br>(Top 3) | rider (8.63%)<br>car (8.05%)<br>bicycle (7.53%) | road (5.16%)<br>rider (3.98%)<br>person (3.51%) |

*Comment:* Motorcycle is rare and confused with rider/car/bicycle in Cityscapes; SYNTHIA tends to mislabel motorcycles as road or rider.
<!-- | Average Representation | 0.08% | 0.21% |
| Average Error | 13.39% | 48.37% | -->

**Samples 1-2:**
| CS Image 1 | CS Image 2 | SYNTHIA Image 1 | SYNTHIA Image 2 |
|-----------|-----------|-----------|----------|
| ![cs_moto_1](assets/cityscapes_class_samples/motorcycle/sample_1_img.png) | ![cs_moto_2](assets/cityscapes_class_samples/motorcycle/sample_2_img.png) | ![synthia_moto_1](assets/synthia_subset_500_class_samples/motorcycle/synthia_sample_1_img.png) | ![synthia_moto_2](assets/synthia_subset_500_class_samples/motorcycle/synthia_sample_2_img.png) |

| CS Label 1 | CS Label 2 | SYNTHIA Label 1 | SYNTHIA Label 2 |
|-----------|-----------|-----------|----------|
| ![cs_moto_1_label](assets/cityscapes_class_samples/motorcycle/sample_1_label.png) | ![cs_moto_2_label](assets/cityscapes_class_samples/motorcycle/sample_2_label.png) | ![synthia_moto_1_label](assets/synthia_subset_500_class_samples/motorcycle/synthia_sample_1_label.png) | ![synthia_moto_2_label](assets/synthia_subset_500_class_samples/motorcycle/synthia_sample_2_label.png) |

<!-- **Samples 3-4:**
| CS Image 3 | CS Image 4 | SYNTHIA Image 3 | SYNTHIA Image 4 |
|-----------|-----------|-----------|----------|
| ![cs_moto_3](assets/cityscapes_class_samples/motorcycle/sample_3_img.png) | ![cs_moto_4](assets/cityscapes_class_samples/motorcycle/sample_4_img.png) | ![synthia_moto_3](assets/synthia_subset_500_class_samples/motorcycle/synthia_sample_3_img.png) | ![synthia_moto_4](assets/synthia_subset_500_class_samples/motorcycle/synthia_sample_5_img.png) |

| CS Label 3 | CS Label 4 | SYNTHIA Label 3 | SYNTHIA Label 4 |
|-----------|-----------|-----------|----------|
| ![cs_moto_3_label](assets/cityscapes_class_samples/motorcycle/sample_3_label.png) | ![cs_moto_4_label](assets/cityscapes_class_samples/motorcycle/sample_4_label.png) | ![synthia_moto_3_label](assets/synthia_subset_500_class_samples/motorcycle/synthia_sample_3_label.png) | ![synthia_moto_4_label](assets/synthia_subset_500_class_samples/motorcycle/synthia_sample_5_label.png) | -->

### 19. Bicycle
| Metric | Cityscapes | SYNTHIA |
|---|---:|---:|
| Representativity | 0.72% | 0.24% |
| IoU | 61.73% | 39.67% |
| Accuracy | 69.81% | 50.16% |
| Error | 30.19% | 49.84% |
| Confused Classes<br>(Top 3) | sidewalk (6.73%)<br>road (5.16%)<br>rider (4.36%) | road (17.78%)<br>sidewalk (11.92%)<br>rider (7.88%) |

*Comment:* Bicycle has low support and moderate error; Cityscapes often confuses bicycles with sidewalk or road, while SYNTHIA strongly confuses them with road. There is a label mismatch: Cityscapes labels pixels inside the wheels as Bicycle, while in SYNTHIA only the wheels and the frame are labeled as Bicycle.
<!-- | Average Representation | 0.70% | 0.24% |
| Average Error | 34.01% | 70.29% | -->

**Samples 1-2:**
| CS Image 1 | CS Image 2 | SYNTHIA Image 1 | SYNTHIA Image 2 |
|-----------|-----------|-----------|----------|
| ![cs_bicycle_1](assets/cityscapes_class_samples/bicycle/sample_1_img.png) | ![cs_bicycle_2](assets/cityscapes_class_samples/bicycle/sample_2_img.png) | ![synthia_bicycle_1](assets/synthia_subset_500_class_samples/bicycle/synthia_sample_1_img.png) | ![synthia_bicycle_2](assets/synthia_subset_500_class_samples/bicycle/synthia_sample_2_img.png) |

| CS Label 1 | CS Label 2 | SYNTHIA Label 1 | SYNTHIA Label 2 |
|-----------|-----------|-----------|----------|
| ![cs_bicycle_1_label](assets/cityscapes_class_samples/bicycle/sample_1_label.png) | ![cs_bicycle_2_label](assets/cityscapes_class_samples/bicycle/sample_2_label.png) | ![synthia_bicycle_1_label](assets/synthia_subset_500_class_samples/bicycle/synthia_sample_1_label.png) | ![synthia_bicycle_2_label](assets/synthia_subset_500_class_samples/bicycle/synthia_sample_2_label.png) |

<!-- **Samples 3-4:**
| CS Image 3 | CS Image 4 | SYNTHIA Image 3 | SYNTHIA Image 4 |
|-----------|-----------|-----------|----------|
| ![cs_bicycle_3](assets/cityscapes_class_samples/bicycle/sample_5_img.png) | ![cs_bicycle_4](assets/cityscapes_class_samples/bicycle/sample_4_img.png) | ![synthia_bicycle_3](assets/synthia_subset_500_class_samples/bicycle/synthia_sample_3_img.png) | ![synthia_bicycle_4](assets/synthia_subset_500_class_samples/bicycle/synthia_sample_4_img.png) |

| CS Label 3 | CS Label 4 | SYNTHIA Label 3 | SYNTHIA Label 4 |
|-----------|-----------|-----------|----------|
| ![cs_bicycle_3_label](assets/cityscapes_class_samples/bicycle/sample_5_label.png) | ![cs_bicycle_4_label](assets/cityscapes_class_samples/bicycle/sample_4_label.png) | ![synthia_bicycle_3_label](assets/synthia_subset_500_class_samples/bicycle/synthia_sample_3_label.png) | ![synthia_bicycle_4_label](assets/synthia_subset_500_class_samples/bicycle/synthia_sample_4_label.png) | -->

## Error vs Scale by Class

The following plot shows error versus object scale (number of pixels) and the scale distribution for each class.

Overall, the object-scale distribution in SYNTHIA is more skewed to the right: objects tend to be smaller in SYNTHIA and larger in Cityscapes. However, this may not hold for the Bicycle class because there is a label mismatch between the datasets.

![scale_plot_error_rate_cityscapes](assets/comparison_scale_plot_error_rate.png)



## Confusion matrix

### Cityscapes (predictions over Cityscapes Validation Set)

The following plot shows the most confused classes. Wall, Fence, Pole, Traffic Light and Traffic Sign are often confused with Building. Road and Sidewalk are often confused with each other.

![syn2cs_cs_confusion_matrix_heatmap](assets/syn2cs_cs_confusion_matrix_heatmap.png) 

### Synthia (Predictions over the subset of Synthia)

In SYNTHIA, classes like pole, traffic light, and traffic sign are often confused with building. Unlike Cityscapes, fence is generally well classified, but bicycle is frequently confused with road and sidewalk.

![syn2cs_gta_confusion_matrix_heatmap](assets/syn2cs_syn_confusion_matrix_heatmap.png)



