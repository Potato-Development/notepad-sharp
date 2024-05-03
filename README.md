# notepad# (notepad-sharp)

![image](https://github.com/Potato-Development/notepad-sharp/assets/119129834/0373a4a3-670d-4ab9-bc87-6c69754f4a64)

## Installation
Check the Wiki (https://github.com/Potato-Development/notepad-sharp/wiki) for more details on installation. Refer to https://git-scm.com/ for the Git docs.
If you know how to, clone the repo and build the code! Feel free to add feature requests, branch/merge code if you have ideas.

1. Download the zip file via the page or this link: https://github.com/Potato-Development/notepad-sharp/archive/refs/heads/main.zip
2. Extract the files to a new folder.
3. Execute (double click) ```setup.exe```. A (usually blue) warning window will appear, titled Windows protected your PC telling you that Microsoft Defender SmartScreen has stopped the installation. Click the underlined "More info" and then "Run anyway" to start the installation. Click the left button if setup is in Japanese (sorry).
4. Once the setup has ended, open the Start Menu and search for ```notepad#```. 

## Source code
For quick access (and reference), the newest fersion of ```Form.cs``` will be pasted here.

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
