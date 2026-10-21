# Barnacle Counter  

Scientists count barnacles in tide pool photos by hand, and one photo can have over 1000. This prototype puts a dot on each barnacle inside the wire frame, so a person only has to check the dots and fix mistakes instead of counting everything.

## Approach
1. **Crop the frame:** find the teal wire by color (HSV), fill gaps with a closing, and take the region in the middle with connected components.
2. **Ground truth:** each outline in the mask goes around the grey middle of a barnacle. Each outline = one barnacle (1500 in img1).
3. **Random forest:** every pixel gets features (color, blur, Sobel edges, lighter/darker than surroundings) and the model learns which pixels are barnacle middles. Each blob it finds = one barnacle.
4. **Scoring:** trained on the left half of img1 and tested on the right half, compared against random dots.
5. **Unseen photo:** used histogram matching to fix the darker lighting.

## Results (right half of img1)
|  | count error | precision | recall |
|---|---|---|---|
| random dots |  | 0.42 | 0.42 |
| random forest | +4% | 0.78 | 0.81 |

Unseen photo: 788 barnacles found before histogram matching, 1255 after.

More details, plots and conclusions are in `barnacles.ipynb`.

## Files
- `barnacles.ipynb`: the whole project, step by step
- `img1.png`, `mask1.png`, `img2.png`, `mask2.png`: labeled photo and its mask
- `unseen_img1.png`, `unseen_img2.png`: photo with no labels

## How to run
1. Install the packages: `pip install opencv-python numpy matplotlib scikit-learn`
2. Keep the images in the same folder as the notebook.
3. Open `barnacles.ipynb` and run all cells (takes a couple of minutes).

## AI use
AI was used to help write the code, debug, and validate steps.
