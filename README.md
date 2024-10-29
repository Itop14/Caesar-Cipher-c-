# Caesar-Cipher-c#

This Caesar cipher, is  both for encoding and decoding. The key is an integer from 1 to 25. This cipher rotates the letters of the alphabet (A to Z). The encoding replaces each letter with the 1st to 25th next letter in the alphabet (wrapping Z to A).

    using System;
    using System.Collections.Generic;
    using System.ComponentModel;
    using System.Data;
    using System.Drawing;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Windows.Forms;

    namespace Caesar_Cipher
    {
        public partial class Form1 : Form
        {
    
            public Form1()
            {
                InitializeComponent();
            }
            private void Decode_btn_Click(object sender, EventArgs e)
            {
                string text = Message.Text; // Makes a string variable called text and contains the message the user has entered
                int key = Convert.ToInt32(Key.Text); // Converts whatever string the user has entered (into the Key Texbox) into an integer 
    
                if (key >= 1 && key <= 25 && (Key.Text != "")) // Make sure the key is valid (between 1 and 25)
                {
                    string encodedmess = Enc_and_Dec(text, -key); // Creates a string variable that will contain our decrypted message (which is done using the Enc_and_Dec function)
                    concls_lab.Text = "Decoded Message: " + encodedmess; // Prints the message
                }
                else { MessageBox.Show("Key has to be between 1 and 25. Please enter a valid key. "); }
            }
    
            private void Encrypt_btn_Click(object sender, EventArgs e)
            {
                string text = Message.Text;// Makes a string variable called text and contains the message the user has entered
                int key = Convert.ToInt32(Key.Text);// Converts whatever string the user has entered (into the Key Texbox) into an integer
    
                if (key >= 1 && key <= 25 && (Key.Text != ""))
                {
                    string encodedmess = Enc_and_Dec(text, key);// Creates a string variable that will contain our decrypted message (which is done using the Enc_and_Dec function)
                    concls_lab.Text = "Encoded Message: " + encodedmess;// Prints the message
                }
                else { MessageBox.Show("Key has to be between 1 and 25. Please enter a valid key. "); }
            }
    
    
    
    
    
            private static string Enc_and_Dec(string text, int jump) // Takes in the message the user has entered and the key
            {
                char[] result = new char[text.Length]; // Creates a list of characters which is the same length as the users message
    
                for (int i = 0; i < text.Length; i++) // iterates through the whole list
                {
                    char letter = text[i];// Reviews the current character 
    
                    if (char.IsLetter(letter)) // Checks if the current character is a letter
                    {
                        char offset = char.IsUpper(letter) ? 'A' : 'a'; // 'A' is the offset for uppercase letters and 'a' is the offset for lowercase
                        result[i] = (char)((letter + jump - offset + 26) % 26 + offset); // Shifts the letter by the jump value and then takes a module of 26 so that the key is in the range 1 to 25
                    }
                    else
                    {
                        result[i] = letter; // Doesnt change anything
                    }
                }
    
                return new string(result);// returns the hidden or decoded message
            }
    
            private void Key_KeyPress(object sender, KeyPressEventArgs e)
            {
                if (!char.IsDigit(e.KeyChar) && !char.IsControl(e.KeyChar)) // checks if the user is typing letters in the box
                {
                    e.Handled = true; // If theyare the letters wont be written in the textbox 
                }
            }
    
            private void label1_Click(object sender, EventArgs e)
            {
    
            }
        }
    }
