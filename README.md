<img width="1024" height="448" alt="Gemini_Generated_Image_npers1npers1nper" src="https://github.com/user-attachments/assets/a1f8ae5b-c9f1-4b22-a22b-18a46c8c2e5c" />

# **Shift Experiment Generator User Guide**

This tool is a Graphical User Interface (GUI) designed to help you construct complex command-line arguments for the `shift_experiment.py` script in the [Distribution Shift Perception Tool](https://github.com/hafeezkhan909/Distribution-Shift-Lane-Perception). It is used for configuring experiments related to **Distribution Shift Lane Perception** without needing to memorize CLI flags.

> ## [Click Here](https://suave101.github.io/Distribution-Shift-Lane-Perception-Command-Generator/) to go to the webpage

## **1. Interface Overview**

The interface is divided into two main areas:

  * **Left Column:** The Configuration Panel where you input your experiment parameters.
  * **Right Column (Sticky):** The Command Output. This updates in real-time as you modify settings on the left.

-----

## **2. Step-by-Step Configuration**

### **A. Dataset Configuration**

This section defines where your data lives and which lists define your train/test splits.

  * **Source Directory:** The root folder for your training/source images (Default: `./datasets/CULane`).
  * **Target Directory:** The root folder for your testing/shifted images (Default: `./datasets/Curvelanes`).
  * **List Paths:** Point these to the text files containing the relative paths of the images for the source and target datasets respectively.

### **B. Sampling & Model Settings**

Configure the scope and hyperparameters of the experiment.

  * **Sample Counts:** Set how many images to sample from the Source (`--src_samples`) and Target (`--tgt_samples`) datasets.
  * **Runs & Calibration:** \* **Num Runs:** How many times to repeat the experiment for statistical significance.
      * **Calibration Runs:** The number of runs dedicated to calibrating the uncertainty quantification.
  * **Hyperparameters:**
      * **Alpha:** Significance level (e.g., 0.05 for 95% confidence).
      * **Image Size/Batch Size:** Adjust according to your GPU memory constraints.
  * **Crop Image:** Check this box to append the `--cropImg` flag (useful if the model expects cropped regions of interest).

### **C. Synthetic Shift Configuration**

This is the core feature for testing robustness against distribution shifts.

1.  **Select Shift Type:** Use the dropdown menu to select the type of shift.

      * **None (Cross-Domain Mode):** Runs the experiment purely between Source and Target datasets without adding synthetic noise.
      * **Synthetic Options:** Gaussian Noise, Rotation, Translation, Shear, Zoom, Horizontal/Vertical Flips.

2.  **Adjust Shift Parameters:**

      * *Note:* Specific input fields will appear based on your selection.
      * **Example:** If you select **Rotation**, a "Rotation Angle" input appears. If you select **Gaussian**, a "Standard Deviation" input appears.

### **D. Logging**

  * **Log Directory:** Folder where results will be saved (Default: `logs`).
  * **Filename:** The name of the JSON file where metrics are recorded (Default: `sanity_check.json`).

-----

## **3. Generating & Running the Command**

Once your configuration is set:

1.  Look at the **Generated Command** card on the right side of the screen.
2.  Click the **Copy Command** button. ( The button will turn green and say "Copied\!" to confirm).
3.  Open your terminal or command prompt.
4.  Navigate to the directory containing `shift_experiment.py`.
5.  Paste the command and hit **Enter**.

**Example Output:**

```bash
python shift_experiment.py \
    --source_dir ./datasets/CULane \
    --target_dir ./datasets/Curvelanes \
    --shift rotation_shift \
    --rotation_angle 15.0 \
    --file_name my_experiment.json
```

-----

## **4. Troubleshooting**

  * **Command Box Empty/Wrong:** Ensure you haven't left required numeric fields blank. The tool uses default values from the HTML if you don't touch them, but deleting a value manually might result in a missing flag.
  * **Copy Button not working:** Ensure your browser allows clipboard access. You can manually highlight the text in the black box and press `Ctrl+C` (Windows) or `Cmd+C` (Mac).

-----
