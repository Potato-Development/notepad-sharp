# notepad# (notepad-sharp)
New version!

![GitHub commit activity](https://img.shields.io/github/commit-activity/t/Potato-Development/notepad-sharp)
![GitHub last commit](https://img.shields.io/github/last-commit/Potato-Development/notepad-sharp)

## Changelog

```
Changelog:
 - Added ai generated, metal themed icons for taskbar applet and window icon!
 - Improved graphics in Windows 11
 - Faster load time by clearing out the Form.Load() and initializeComponent
 - Titlebar now shows file name and path of open file and "Untitled" with a new file. These are seperated with a dash from the application name. 
 - 3D border around the main textbox.
```
[image](https://github.com/Potato-Development/notepad-sharp/assets/119129834/c0afbebd-ab4a-41ba-8501-b5e04b4d11e5)

## Installation
Check the Wiki (https://github.com/Potato-Development/notepad-sharp/wiki) for more details on installation. Refer to https://git-scm.com/ for the Git docs.
If you know how to, clone the repo and build the code! Feel free to add feature requests, branch/merge code if you have ideas.

1. Download the zip file via the page or this link: https://github.com/Potato-Development/notepad-sharp/archive/refs/heads/main.zip
2. Extract the files to a new folder.
3. Execute (double click) ```setup.exe```. A (usually blue) warning window will appear, titled Windows protected your PC telling you that Microsoft Defender SmartScreen has stopped the installation. Click the underlined "More info" and then "Run anyway" to start the installation. Click the left button if setup is in Japanese (sorry).
4. Once the setup has ended, open the Start Menu and search for ```notepad#```. 

## Source code
For quick access (and reference), the newest version of ```Form.cs``` will be pasted in the code block below.

```
using System.Windows.Forms;

namespace notepad_sharp
{
    public partial class Form : System.Windows.Forms.Form
    {
        private bool isFileModified = false;
        private string currentFilePath = "";
        public Form()
        {
            InitializeComponent();
            UpdateTitle();
        }

        private void UpdateTitle()
        {
            string fileName = string.IsNullOrEmpty(currentFilePath) ? "Untitled" : Path.GetFileName(currentFilePath);
            this.Text = fileName + " - Notepad#";
        }

        //exit
        private void exitXToolStripMenuItem_Click(object sender, EventArgs e)
        {
            if (isFileModified)
            {
                PromptToSaveChanges();
            }
            else
            {
                Application.Exit();
            }
        }


        //new
        private void newNToolStripMenuItem_Click(object sender, EventArgs e)
        {
            if (isFileModified)
            {
                PromptToSaveChanges();
            }
            else
            {
                richTextBox.Text = "";
                currentFilePath = "";
                isFileModified = false;
                UpdateTitle();
            }
        }

        private void toolStripButton1_Click(object sender, EventArgs e)
        {
            if (isFileModified)
            {
                PromptToSaveChanges();
            }
            else
            {
                richTextBox.Text = "";
                currentFilePath = "";
                isFileModified = false;
                UpdateTitle();
            }
        }


        //open
        private void openOToolStripMenuItem_Click(object sender, EventArgs e)
        {
            if (isFileModified)
            {
                PromptToSaveChanges();
            }
            else
            {
                OpenFile();
            }
        }
        private void toolStripButton2_Click(object sender, EventArgs e)
        {
            if (isFileModified)
            {
                PromptToSaveChanges();
            }
            else
            {
                OpenFile();
            }
        }
        private void OpenFile()
        {
            OpenFileDialog openFileDialog = new OpenFileDialog();
            if (openFileDialog.ShowDialog() == DialogResult.OK)
            {
                richTextBox.Text = File.ReadAllText(openFileDialog.FileName);
                currentFilePath = openFileDialog.FileName;
                isFileModified = false;
                UpdateTitle();
            }
        }


        //save and save as
        private void saveSToolStripMenuItem_Click(object sender, EventArgs e)
        {
            if (string.IsNullOrEmpty(currentFilePath))
            {
                SaveAs();
            }
            else
            {
                SaveToFile(currentFilePath);
            }
        }

        private void toolStripButton3_Click(object sender, EventArgs e)
        {
            if (string.IsNullOrEmpty(currentFilePath))
            {
                SaveAs();
            }
            else
            {
                SaveToFile(currentFilePath);
            }
        }

        private void saveAsAToolStripMenuItem_Click(object sender, EventArgs e)
        {
            SaveAs();
        }

        private void SaveAs()
        {
            SaveFileDialog saveFileDialog = new SaveFileDialog();
            if (saveFileDialog.ShowDialog() == DialogResult.OK)
            {
                SaveToFile(saveFileDialog.FileName);
            }
        }
        private void SaveToFile(string filePath)
        {
            File.WriteAllText(filePath, richTextBox.Text);
            currentFilePath = filePath;
            isFileModified = false;
            UpdateTitle();
        }



        //cut
        private void cutXToolStripMenuItem_Click(object sender, EventArgs e)
        {
            richTextBox.Cut();
        }

        private void toolStripButton4_Click(object sender, EventArgs e)
        {
            richTextBox.Cut();
        }


        //copy
        private void copyCToolStripMenuItem_Click(object sender, EventArgs e)
        {
            richTextBox.Copy();
        }

        private void toolStripButton5_Click(object sender, EventArgs e)
        {
            richTextBox.Copy();
        }


        //paste
        private void pastePToolStripMenuItem_Click(object sender, EventArgs e)
        {
            richTextBox.Paste();
        }

        private void toolStripButton6_Click(object sender, EventArgs e)
        {
            richTextBox.Paste();
        }

        //prompt to save changes
        private void PromptToSaveChanges()
        {
            DialogResult result = MessageBox.Show("Do you want to save changes?", "Confirmation", MessageBoxButtons.YesNoCancel);
            if (result == DialogResult.Yes)
            {
                if (string.IsNullOrEmpty(currentFilePath))
                {
                    SaveAs();
                }
                else
                {
                    SaveToFile(currentFilePath);
                }
            }
            else if (result == DialogResult.No)
            {
                // Don't save changes, proceed with the action
                isFileModified = false;
            }
            // If Cancel, do nothing and keep the dialog open
        }

        private void richTextBox_TextChanged(object sender, EventArgs e)
        {
            isFileModified = true;
        }
    }
}

```
