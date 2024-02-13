using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace convertidor_de_temperaturas
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void btnConvertidor_Click(object sender, EventArgs e)
        {
            {
                if (string.IsNullOrWhiteSpace(txtTemperatura.Text))
                {
                    MessageBox.Show("Ingrese un valor de temperatura.", "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                    return;
                }

                double temperatura;
                if (!double.TryParse(txtTemperatura.Text, out temperatura))
                {
                    MessageBox.Show("Ingrese un valor numérico válido.", "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                    return;
                }

                double result;
                string fromUnit = cmbSeleccion.SelectedItem.ToString();
                string toUnit = cmbSeleccion2.SelectedItem.ToString();

                if (fromUnit == "Fahrenheit" && toUnit == "Celsius")
                {
                    result = (temperatura - 32) * 5 / 9;
                }
                else if (fromUnit == "Fahrenheit" && toUnit == "Kelvin")
                {
                    result = (temperatura + 459.67) * 5 / 9;
                }
                else if (fromUnit == "Celsius" && toUnit == "Fahrenheit")
                {
                    result = (temperatura * 9 / 5) + 32;
                }
                else if (fromUnit == "Celsius" && toUnit == "Kelvin")
                {
                    result = temperatura + 273.15;
                }
                else if (fromUnit == "Kelvin" && toUnit == "Fahrenheit")
                {
                    result = (temperatura * 9 / 5) - 459.67;
                }
                else if (fromUnit == "Kelvin" && toUnit == "Celsius")
                {
                    result = temperatura - 273.15;
                }
                else
                {
                    MessageBox.Show("Seleccione unidades válidas para la conversión.", "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                    return;
                }

                txtResultado.Text = result.ToString();
            }
        }

        private void btnLimpiardatos_Click(object sender, EventArgs e)
        {
            txtTemperatura.Text = string.Empty;
            txtResultado.Text = string.Empty;
            cmbSeleccion.Text = string.Empty;
            cmbSeleccion2.Text = string.Empty;
        }
    }
}

