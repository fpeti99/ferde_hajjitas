using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace ferde_hajjitas
{
    public partial class Form1 : Form
    {
        Madar m;
        const double g = 9.81;
        double dt = 0.02;

        public Form1()
        {
            InitializeComponent();
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            m = new Madar(button1);
        }

        private void timer1_Tick(object sender, EventArgs e)
        {
            m.lep(dt, g);
        }

        private void button2_Click(object sender, EventArgs e)
        {
            int szog, seb;
            m.x = 0;
            m.y = Height;


            if(!int.TryParse(textBox1.Text, out szog))
            {
                MessageBox.Show("Hiba a konverzióban!");
                return;
            }

            //szog = int.Parse(textBox1.Text);
            if(!int.TryParse(textBox2.Text, out seb))
            {
                MessageBox.Show("Hiba a konverzióban!");
            }
            //seb = int.Parse(textBox2.Text);

            m.dx = seb * Math.Cos(szog*(Math.PI/180));
            m.dy = -seb * Math.Sin(szog * (Math.PI / 180));

            timer1.Interval = (int)(dt * 1000);

            timer1.Start();
        }
    }
}




using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using System.Drawing;

namespace ferde_hajjitas
{
    class Madar
    {
        public double x, y, dx, dy;
        public Button gomb;

        public Madar(Button b)
        {
            b.BackColor = Color.Red;
            gomb = b;
        }

        public void lep(double dt, double g)
        {
            x += dx;
            y += dy;
            dy += dt * g;
            gomb.Left = (int)x;
            gomb.Top = (int)y;
        }

    }
}






