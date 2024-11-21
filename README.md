using System;
using System.Windows.Forms;

namespace WinFormsApp
{
    public class MainForm : Form
    {
        public MainForm()
        {
            Text = "Главная форма";
            Width = 400;
            Height = 200;

            Button subscriptionButton = new Button
            {
                Text = "Форма подписки",
                Top = 20,
                Left = 20,
                Width = 150
            };
            subscriptionButton.Click += (s, e) =>
            {
                var subscriptionForm = new SubscriptionForm();
                subscriptionForm.ShowDialog();
            };
            Controls.Add(subscriptionButton);

            Button lengthConversionButton = new Button
            {
                Text = "Перевод длины",
                Top = 60,
                Left = 20,
                Width = 150
            };
            lengthConversionButton.Click += (s, e) =>
            {
                var lengthForm = new LengthConversionForm();
                lengthForm.ShowDialog();
            };
            Controls.Add(lengthConversionButton);

            Button ticketOrderButton = new Button
            {
                Text = "Заказ билетов",
                Top = 100,
                Left = 20,
                Width = 150
            };
            ticketOrderButton.Click += (s, e) =>
            {
                var ticketForm = new TicketOrderForm();
                ticketForm.ShowDialog();
            };
            Controls.Add(ticketOrderButton);
        }

        [STAThread]
        static void Main()
        {
            Application.EnableVisualStyles();
            Application.Run(new MainForm());
        }
    }
}





using System;
using System.Windows.Forms;

namespace WinFormsApp
{
    public class LengthConversionForm : Form
    {
        public LengthConversionForm()
        {
            Text = "Перевод длины в метры";
            Width = 400;
            Height = 300;

            Label inputLabel = new Label
            {
                Text = "Введите длину:",
                Top = 20,
                Left = 20
            };
            Controls.Add(inputLabel);

            TextBox inputTextBox = new TextBox
            {
                Top = 20,
                Left = 120,
                Width = 150
            };
            Controls.Add(inputTextBox);

            GroupBox unitGroupBox = new GroupBox
            {
                Text = "Выберите единицу измерения:",
                Top = 60,
                Left = 20,
                Width = 250,
                Height = 130
            };

            RadioButton inchesRadio = new RadioButton
            {
                Text = "Дюймы",
                Top = 20,
                Left = 10
            };
            unitGroupBox.Controls.Add(inchesRadio);

            RadioButton kilometersRadio = new RadioButton
            {
                Text = "Километры",
                Top = 50,
                Left = 10,
                Checked = true
            };
            unitGroupBox.Controls.Add(kilometersRadio);

            RadioButton centimetersRadio = new RadioButton
            {
                Text = "Сантиметры",
                Top = 80,
                Left = 10
            };
            unitGroupBox.Controls.Add(centimetersRadio);

            RadioButton feetRadio = new RadioButton
            {
                Text = "Футы",
                Top = 110,
                Left = 10
            };
            unitGroupBox.Controls.Add(feetRadio);

            Controls.Add(unitGroupBox);

            Button convertButton = new Button
            {
                Text = "Перевести",
                Top = 200,
                Left = 20
            };
            Controls.Add(convertButton);

            Label resultLabel = new Label
            {
                Text = "Результат: ",
                Top = 240,
                Left = 20,
                Width = 300
            };
            Controls.Add(resultLabel);

            convertButton.Click += (s, e) =>
            {
                if (double.TryParse(inputTextBox.Text, out double value))
                {
                    double result = 0;
                    if (kilometersRadio.Checked) result = value * 1000;
                    else if (centimetersRadio.Checked) result = value / 100;
                    else if (inchesRadio.Checked) result = value * 0.0254;
                    else if (feetRadio.Checked) result = value * 0.3048;

                    resultLabel.Text = $"Результат: {result} метров";
                }
                else
                {
                    MessageBox.Show("Введите корректное число!");
                }
            };
        }
    }
}










using System;
using System.Windows.Forms;

namespace WinFormsApp
{
    public class TicketOrderForm : Form
    {
        public TicketOrderForm()
        {
            Text = "Заказ билетов";
            Width = 400;
            Height = 300;

            Label fromLabel = new Label
            {
                Text = "Город вылета:",
                Top = 20,
                Left = 20
            };
            Controls.Add(fromLabel);

            TextBox fromTextBox = new TextBox
            {
                Top = 20,
                Left = 120,
                Width = 200
            };
            Controls.Add(fromTextBox);

            Label toLabel = new Label
            {
                Text = "Город прилета:",
                Top = 60,
                Left = 20
            };
            Controls.Add(toLabel);

            TextBox toTextBox = new TextBox
            {
                Top = 60,
                Left = 120,
                Width = 200
            };
            Controls.Add(toTextBox);

            Label departureLabel = new Label
            {
                Text = "Дата вылета:",
                Top = 100,
                Left = 20
            };
            Controls.Add(departureLabel);

            DateTimePicker departurePicker = new DateTimePicker
            {
                Top = 100,
                Left = 120
            };
            Controls.Add(departurePicker);

            Label returnLabel = new Label
            {
                Text = "Дата возврата:",
                Top = 140,
                Left = 20
            };
            Controls.Add(returnLabel);

            DateTimePicker returnPicker = new DateTimePicker
            {
                Top = 140,
                Left = 120,
                ShowCheckBox = true
            };
            Controls.Add(returnPicker);

            Button orderButton = new Button
            {
                Text = "Заказать",
                Top = 200,
                Left = 20
            };
            Controls.Add(orderButton);

            Label resultLabel = new Label
            {
                Text = "",
                Top = 240,
                Left = 20,
                Width = 350
            };
            Controls.Add(resultLabel);

            orderButton.Click += (s, e) =>
            {
                string from = fromTextBox.Text;
                string to = toTextBox.Text;
                string departure = departurePicker.Value.ToShortDateString();
                string result = $"Билет: {departure} {from} - {to}";

                if (returnPicker.Checked)
                {
                    string returnDate = returnPicker.Value.ToShortDateString();
                    result += $"\nОбратный билет: {returnDate} {to} - {from}";
                }

                resultLabel.Text = result;
            };
        }
    }
}
