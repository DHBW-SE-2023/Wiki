# Image Processing 23, 21, 24, 25, 36, 49, 58

- Paper sheet detection
- Reverse perspective transform
- Table detection
- Row/Column detection
- Printed text detection (left column)
- Detection of valid signature fields (only one signature per field, no overlaps, can it qualify as a signature)
- Extraction of list of user and if valid signature is present


# Step 1 - Find the table and warp the perspective

## Description

The first step of the image pipeline is to find the table the program is interested in. The image of the sheet of paper with the table of students along with their signatures on it is taken by a mobile device. Therefore the image contains more than the sheet of paper itself (e.g. the desk underneath it).
Another problem poses the tilt the image might be taken at, which could mess with the further steps in the pipeline.
The image has to be transformed in such way, that only the table is in the image and that the image is shown from an orthogonal view (think CamScanner for the mobile phone).

To achieve this the first step needed is to detect the table. It is to assume that the largest rectangle with black borders can be found and the step of finding the sheet of paper first can be skipped. That is because most desks in the DHBW have a white surface, therefore the paper blends in with the table and we can instantly retrieve the largest rectangle. This might portray a future source of errors.
Tthe contour of the largest rectangle, which is the table with the signatures, can be used to do a WarpPerspective on the image (effectively a reverse perspective transform) which does the desired transformation of the original image.

## Criteria for acceptance

Image is given

- Find the largest black rectangle
- Transform it to reverse perspective 
- result shows table from an orthogonal view
- resulting image only consists of the table

## Execution

To start with image processing, we should use a new module. The module is called cv (short for computer vision). It contains all code of our application responsible for doing any kind of image processing.
The module's code should be used only internally, its library functions are not stable and could change at any moment. Therefore we put it in the internal/ folder.
The path for the module is therefore internal/cv.

# Step 2 - Extract the table's information ( \#44 - cell extraction out of table?)

## Description

The second major step of the image processing pipeline. The starting point is an image that shows the table of the students' names and the signatures. This table is presented from an orthogonal view to ease further processing.
At first the image needs to be converted to a binary image. This is the preparation which occurs before the extraction of the table itself starts.
Then the horizontal and vertical lines that make up the table grid will get extracted and the image with the horizontal and vertical kernels (of the form Nx1 and 1xN, respectively) will be opened. After recombining the vertical and horizontal lines, all  contours get extracted.
The contours are sorted into an [rows][cols]image.Rectangle from top left to bottom right. Then any undesirable columns (mainly those that have a zero width or height) get filtered out.
The resulting columns together with the image are saved in a struct.

## Criteria for acceptance

- Take in image
- Build table struct from data shown in image
- Table contains its cells in a matrix of the image
- Rectangles in row-major
- Reliable identification of cells of a table 
- Table for a TI list should always have 3 columns
- Logic for creating a table from an image is responsible for providing that result

## Execution

Unfortunately, the module's library functions are not stable and could change at any moment. Therefore the code should be used only internally, which is why it was put in the internal/ folder. The path for the module is internal/cv.

# Step 3 - Get the student's names from the table

## Description

Take in a preprocessed image along with the Table struct describing the shown table. Assume the second column (index 1) to be the column containing the names of the students by convention. Recognize the printed names and accumulate them into a list.
To do the image recognition we use the OCRTesseract library along via its Golang bindings (gosseract).

## Criteria for acceptance

Preprocessed image is given: grayscale, denoised, has a Gaussian blur to deal with remaining noise, has accompanying Table struct

- Extract printed student names shown in the table in the shown order of the image
- Order must be contained

## Execution

The text recognition is still pretty bad. Maybe by creating a custom language file and telling Gosseract to use it performance would be increased. The downside here is that for every new year this language file would have to be automatically generated.

# Step 4: Signature validation

## Description

For all rows with a student name, extract the signature field, which is located on its right. Column 2 contains the student's name while column 3 contains the signatures. Check for each signature field if the there is only one signature in the signature column. If there is not exactly one signature detected in each signature field, mark the row as invalid.
The detecting is performed by finding all contours in the signature field image, then getting the bounding boxes of them. For each bounding box it is checked if the bounding box has a minimum size, else it will be skipped. The next step is to check if the count of the remaining bounding boxes is equal to 1 and if so the column is marked as valid, else it is marked as invalid.

## Criteria for acceptance

BGR image is given

- Show signature field
- Detect all signatures in the image
- If not exactly one signature was detected, mark the row as invalid
- Accuracy must be at 100%

## Execution

Bounding boxes that are relatively close together into a single bounding box, should also be contracted, as the most definitely belong to the same signature. They should be contracted if they have a dx of less or equal to 1% of the max width.

This is done via the function cv.ValidSignature, which returns a boolean, true if the signature is valid, false if it is invalid.
It does this by finding the contours and getting the bounding boxes of them. It skips all bounding boxes that are to small. It checks that the count of every properly sized bounding box is equal to one, i.e. only one signature is present.

An additional check was added for when a signature would be split apart, because the signature would consist of multiple non-touching parts. Now all bounding rectangles are attempted to merge with other nearby bounding rectangles. This process has completed only once, the previous algorithm is applied on the merged rectangles.
This solves previous issues, where a signature was deemed invalid, because cv.ValidSignature was only looking at individual bounding rectangles.