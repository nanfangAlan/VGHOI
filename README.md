# Visual-Guided Human-Object Interaction Detection (VG-HOI)

This repository contains the code and dataset split for our paper on **Visual-Guided Human-Object Interaction (HOI) Detection**. Our approach leverages visual support examples to detect unseen HOI categories, offering a practical alternative to text-based methods in scenarios where language descriptions are ambiguous or unavailable.

## News
*   **[September 2025]** Dataset split released.

## Abstract
Detecting unseen Human-Object Interactions (HOIs) is a critical challenge in open-world scenarios. Existing methods heavily rely on text-based priors from large vision-language models (VLMs), which can be unreliable for fine-grained or domain-specific interactions. We introduce a novel **Visual-Guided HOI (VG-HOI)** detection task, where a model learns to recognize novel HOIs using a single visual support image per category, without retraining. Our approach extracts human, object, and union prototypes from the support image and uses them to guide the query image's feature extraction via cross-attention, enabling effective generalization to unseen interactions.
<img width="5376" height="2453" alt="model" src="https://github.com/user-attachments/assets/24cdd77f-7f6a-4e82-b217-aec4f42a9558" />


## Main Results
Our model achieves state-of-the-art performance on our extended HICO-DET benchmark for unseen HOI generalization.

| Model | Base (mAP) | UC (mAP) | UO (mAP) | UV (mAP) | UOUV (mAP) | Full (mAP) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **VG-HOI (Ours)** | **40.47** | **37.44** | **19.50** | **40.43** | **20.84** | **34.78** |
| GEN-VLKT | 38.12 | 33.28 | 17.85 | 38.01 | 18.15 | 33.28 |

*UC: Unseen Composition, UO: Unseen Object, UV: Unseen Verb, UOUV: Unseen Object & Unseen Verb.*

## Dataset: HICO-DET

### Introduction
HICO-DET is a large-scale dataset for HOI detection. It contains:
*   **600 HOI Categories**: Defined as `<verb, object>` pairs.
*   **117,766 Images**: With a total of 47,766 annotated images.
*   **152,463 HOI Instances**: Each annotated with human and object bounding boxes.
*   **80 Object Categories**: And 117 verb categories.

The dataset is divided into a **training set** (38,118 images) and a **testing set** (9,648 images).

### Download Instructions
1.  **Images and Annotations**: Download the HICO-DET dataset from the official website:
    [http://www-personal.umich.edu/~ywchao/hico/](http://www-personal.umich.edu/~ywchao/hico/)
    This will give you the `hico_20160224_det` folder.

2.  **Our Extended Split**: Download our dataset split files from our GitHub repository:
    [https://github.com/your-username/VG-HOI](https://github.com/your-username/VG-HOI)
    Place the downloaded split files into the `hico_20160224_det` directory.

### Dataset Structure
After downloading and placing the split files, your dataset directory should look like this:

```
hico_20160224_det/
├── annotations/
│   ├── trainval_hico.json
│   └── test_hico.json
├── images/
│   ├── train2015/
│   └── val2015/
├── hoi_list.json
├── object_list.json
├── verb_list.json
├── _split.json_/
└── ... (other original files)
```

### Our Split for VG-HOI Benchmark
We extend HICO-DET by splitting its 600 HOI categories into a **base set** and four **novel sets** to evaluate different aspects of generalization.

| Split Name | Description | Number of Categories | HOI IDs |
| :--- | :--- | :--- | :--- |
| **Base Set** | HOIs used for training. | 267 | `[0, 3, 4, 6, 9, 10, 11, 12, 13, 14, 16, 17, 18, 20, 21, 24, 26, 27, 28, 29, 30, 86, 87, 90, 91, 97, 98, 99, 100, 101, 102, 104, 105, 107, 108, 109, 111, 112, 116, 117, 118, 121, 123, 124, 131, 132, 133, 134, 137, 138, 142, 146, 147, 148, 151, 153, 155, 156, 157, 160, 161, 162, 164, 165, 166, 167, 169, 174, 178, 179, 180, 183, 185, 194, 195, 196, 208, 210, 211, 212, 214, 215, 216, 218, 219, 220, 221, 222, 224, 225, 226, 227, 229, 230, 231, 236, 237, 238, 247, 249, 250, 252, 253, 264, 265, 266, 269, 270, 272, 283, 286, 287, 289, 290, 291, 292, 294, 295, 297, 298, 299, 302, 304, 305, 309, 325, 327, 328, 329, 330, 331, 332, 335, 336, 337, 338, 343, 344, 345, 346, 347, 348, 350, 351, 352, 353, 354, 355, 356, 360, 363, 365, 366, 368, 369, 370, 374, 383, 387, 389, 390, 392, 393, 394, 395, 396, 397, 400, 407, 408, 409, 410, 411, 413, 414, 415, 416, 417, 418, 419, 424, 426, 428, 429, 431, 432, 433, 434, 435, 437, 438, 442, 449, 450, 453, 454, 455, 456, 461, 462, 463, 465, 466, 467, 469, 470, 471, 472, 473, 474, 475, 476, 480, 481, 482, 483, 488, 489, 490, 491, 493, 495, 497, 498, 500, 502, 503, 504, 505, 506, 509, 511, 512, 514, 515, 516, 518, 519, 520, 523, 524, 528, 529, 530, 538, 539, 542, 543, 545, 546, 548, 558, 559, 561, 563, 564, 565, 569, 575, 584, 585, 586, 587, 588, 596, 597, 599]` |
| **UC (Unseen Composition)** | Novel combinations of seen verbs and objects. | 89 | `[23, 103, 106, 110, 115, 119, 120, 125, 127, 128, 136, 139, 140, 141, 143, 145, 149, 152, 159, 163, 176, 177, 181, 197, 209, 213, 223, 248, 251, 256, 268, 284, 285, 301, 306, 308, 311, 312, 326, 340, 341, 358, 361, 362, 364, 367, 371, 372, 375, 384, 385, 386, 388, 398, 401, 402, 403, 406, 421, 423, 427, 430, 440, 443, 444, 452, 457, 459, 464, 477, 478, 479, 487, 494, 501, 508, 527, 531, 532, 540, 541, 544, 549, 566, 571, 572, 589, 594, 598]` |
| **UO (Unseen Object)** | Seen verbs applied to novel objects. | 102 | `[31, 34, 35, 37, 38, 39, 40, 42, 43, 45, 46, 48, 49, 51, 52, 53, 54, 58, 60, 63, 64, 65, 68, 69, 70, 73, 75, 76, 78, 79, 80, 81, 84, 85, 92, 95, 170, 171, 172, 173, 186, 190, 193, 198, 199, 201, 202, 203, 204, 205, 207, 232, 233, 234, 239, 242, 243, 246, 257, 259, 260, 261, 263, 273, 275, 277, 278, 279, 280, 282, 314, 315, 316, 317, 318, 319, 320, 321, 323, 324, 377, 378, 380, 382, 446, 447, 448, 533, 534, 535, 537, 550, 552, 553, 555, 557, 576, 577, 579, 580, 582, 583]` |
| **UV (Unseen Verb)** | Novel verbs applied to seen objects. | 91 | `[1, 2, 5, 7, 8, 15, 19, 22, 25, 88, 89, 96, 113, 114, 122, 126, 129, 130, 135, 144, 150, 154, 158, 168, 175, 182, 184, 217, 228, 235, 254, 255, 267, 271, 288, 293, 296, 300, 303, 307, 310, 333, 334, 339, 342, 349, 357, 359, 373, 391, 399, 404, 405, 412, 420, 422, 425, 436, 439, 441, 451, 458, 460, 468, 484, 485, 486, 492, 496, 499, 507, 510, 513, 517, 521, 522, 525, 526, 547, 560, 562, 567, 568, 570, 573, 574, 590, 591, 592, 593, 595]` |
| **UOUV (Unseen Object & Verb)** | Novel combinations of novel verbs and objects. | 51 | `[32, 33, 36, 41, 44, 47, 50, 55, 56, 57, 59, 61, 62, 66, 67, 71, 72, 74, 77, 82, 83, 93, 94, 187, 188, 189, 191, 192, 200, 206, 240, 241, 244, 245, 258, 262, 274, 276, 281, 313, 322, 376, 379, 381, 445, 536, 551, 554, 556, 578, 581]` |

The code will be released as soon as possible.

## Acknowledgements
We thank the authors of HICO-DET and GEN-VLKT for their valuable datasets and codebases.
