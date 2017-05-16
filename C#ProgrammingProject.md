using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace ISYS250Project1
{

    public partial class frmInventory : Form
    {
        private static frmInventory frminventory = new frmInventory(); //creates a private static instance of the inventory form

        public static frmInventory frmInventories //creates a public instance of the private instance we created before so that one single form can be accessed from frmOrder
        {
            get { return frminventory; } //get;set values for the form
            set { frminventory = value; }
        }
       
        public frmInventory()
        {
            InitializeComponent();
        }
        
        public static string[] initialItems = new string[18] { "Flour", "Yeast", "Sugar", "Oil", "Ham", "Turkey", "Scheese", "Lettuce", "Tomato", "Bacon", "Pickles", "Mayo", "Mustard", "Pepperoni", "Sauce", "gCheese", "Salt", "Pepper" };
        int[] initialAmounts = new int[18] { 200, 50, 30, 25, 10, 10, 20, 14, 14, 10, 20, 15, 12, 20, 60, 25, 10, 10 };
        decimal[,] itemUnits = new decimal[18, 6] { { 1m, 1m, 1m, 3m, 3m, 3m }, { 0.5m, 0.5m, 0.5m, 2m, 2m, 2m }, { 0.03m, 0.03m, 0.03m, 0.5m, 0.5m, 0.5m }, { 0.05m, 0.05m, 0.05m, 0.1m, 0.1m, 0.1m }, { 0.1m, 0m, 0m, 0m, 0m, 0.1m }, { 0m, 0.1m, 0m, 0m, 0m, 0.1m }, { 0.1m, 0.1m, 0m, 0m, 0m, 0m }, { 0.25m, 0.25m, 0.3m, 0m, 0m, 0m }, { 0.25m, 0.25m, 0.3m, 0m, 0m, 0.3m }, { 0m, 0m, 0.1m, 0m, 0m, 0.1m }, { 0.02m, 0.02m, 0m, 0m, 0m, 0m }, { 0.02m, 0.02m, 0.02m, 0m, 0m, 0m }, { 0.02m, 0.02m, 0.02m, 0m, 0m, 0m }, { 0m, 0m, 0m, 0m, 0.3m, 0.3m }, { 0m, 0m, 0m, 1m, 1m, 1m }, { 0m, 0m, 0m, 0.3m, 0.2m, 0.2m }, { 0.01m, 0.01m, 0.01m, 0.02m, 0.02m, 0.02m }, { 0.01m, 0.01m, 0.01m, 0.02m, 0.02m, 0.02m } };
        decimal[] currentAmounts = new decimal[18] { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 };

        public Array InitialItems //get for the array initialItems so that it can be accessed in frmOrder
        {
            get
            {
                return initialItems;
            }
        }


        public int lstInventorySelectedIndex //get/set for the lstInventory selected index to be used in determining which column to use in the itemUnits array
        {
            get
            {
                return lstInventory.SelectedIndex = 0;
            }
            set
            {
                lstInventory.SelectedIndex = value;
            }

        }
        /// <summary>
        /// this method will provide the listboxes with their initial information
        /// </summary>
        public void LoadInventoryListBox()
        {
            for (int i = 0; i < initialItems.Length; i++) //for loop to get the initial state of the listboxes on frmInventory
            {
                lstInventory.Items.Add(initialItems[i] + ": " + initialAmounts[i]);
                lstIngredientsUsed.Items.Add(initialItems[i] + ": " + currentAmounts[i]);
            }
        }

        /// <summary>
        /// 
        /// </summary>
        /// <param name="sender"></param>
        /// <param name="e"></param>
        private void frmInventory_FormClosing(object sender, FormClosingEventArgs e) //if the form closes, the inventory form instance is gone and we get errors. So we hide instead of closing to prevent errors
        {
            if (e.CloseReason == CloseReason.UserClosing) //if the user tries to close the form(ex. pressing the x button)
            {
                e.Cancel = true;
                Hide(); //predefined method to hide the control of the event, in this case the inventory form
            }
        }

        /// <summary>
        /// this method will show the vendor form when the vendor button is clicked 
        /// </summary>
        /// <param name="sender"></param>
        /// <param name="e"></param>
        private void btnVendors_Click(object sender, EventArgs e)
        {
            frmVendor newVendorForm = new frmVendor(); //creates a new frm Vendor form
            newVendorForm.ShowDialog(); //shows the form as a dialog box


        }

    }
}

