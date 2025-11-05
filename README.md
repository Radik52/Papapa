using System;
using System.Drawing;
using System.Windows.Forms;

public class Form1 : Form
{
    private Label lblPrompt;
    private TextBox txtNumber;
    private Button btnCompute;
    private Label lblResult;

    public Form1()
    {
        InitializeComponent();
    }

    private void InitializeComponent()
    {
        this.Text = "Сумма цифр (n ≤ 100)";
        this.ClientSize = new Size(420, 150);
        this.FormBorderStyle = FormBorderStyle.FixedDialog;
        this.MaximizeBox = false;

        lblPrompt = new Label() { Text = "Введите натуральное число n (1..100):", Location = new Point(12, 12), AutoSize = true };
        txtNumber = new TextBox() { Location = new Point(15, 35), Width = 120, Name = "txtNumber" };
        btnCompute = new Button() { Text = "Вычислить сумму цифр", Location = new Point(150, 33), AutoSize = true };
        lblResult = new Label() { Text = "Сумма цифр: ", Location = new Point(12, 80), AutoSize = true, Font = new Font(FontFamily.GenericSansSerif, 10, FontStyle.Bold) };

        btnCompute.Click += btnCompute_Click;

        this.Controls.Add(lblPrompt);
        this.Controls.Add(txtNumber);
        this.Controls.Add(btnCompute);
        this.Controls.Add(lblResult);
    }

    private void btnCompute_Click(object sender, EventArgs e)
    {
        if (!int.TryParse(txtNumber.Text.Trim(), out int n))
        {
            MessageBox.Show("Введите целое число.", "Ошибка", MessageBoxButtons.OK, MessageBoxIcon.Warning);
            return;
        }

        if (n < 1 || n > 100)
        {
            MessageBox.Show("Число должно быть натуральным и в диапазоне 1..100.", "Ошибка", MessageBoxButtons.OK, MessageBoxIcon.Warning);
            return;
        }

        int temp = n;
        int sum = 0;
        while (temp > 0)
        {
            sum += temp % 10;
            temp /= 10;
        }

        lblResult.Text = $"Сумма цифр: {sum}";
    }
}
