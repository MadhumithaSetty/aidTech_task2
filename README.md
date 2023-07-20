# aidTech_task2

Temperature Conversion

Create a program that can convert temperature between Celsius, Fahrenheit, and Kelvin scales.

Steps to create the project:

1. Create a user interface using Java Swing or JavaFX to display the temperature conversion utility and capture user input.

2. Implement methods to convert temperature between Celsius, Fahrenheit, and Kelvin scales.

3. Use exception handling to handle errors, such as entering invalid input

4. Add a button to clear the utility display and reset the conversion.

5. Add a button to switch between Celsius, Fahrenheit, and Kelvin scales.


CODE:
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class TemperatureConverter extends JFrame {
    /**
	 * 
	 */
	private static final long serialVersionUID = 1L;
	private JTextField inputField, resultField;
    private JRadioButton celsiusRadio, fahrenheitRadio, kelvinRadio;

    public TemperatureConverter() {
        setTitle("Temperature Converter");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new GridLayout(4, 2, 10, 10));
        setResizable(false);

        JLabel inputLabel = new JLabel("Temperature:");
        add(inputLabel);

        inputField = new JTextField(10);
        add(inputField);

        celsiusRadio = new JRadioButton("Celsius");
        celsiusRadio.setSelected(true);
        add(celsiusRadio);

        fahrenheitRadio = new JRadioButton("Fahrenheit");
        add(fahrenheitRadio);

        kelvinRadio = new JRadioButton("Kelvin");
        add(kelvinRadio);

        ButtonGroup radioGroup = new ButtonGroup();
        radioGroup.add(celsiusRadio);
        radioGroup.add(fahrenheitRadio);
        radioGroup.add(kelvinRadio);

        JButton convertButton = new JButton("Convert");
        convertButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                convertTemperature();
            }
        });
        add(convertButton);

        JButton clearButton = new JButton("Clear");
        clearButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                inputField.setText("");
                resultField.setText("");
            }
        });
        add(clearButton);

        resultField = new JTextField(10);
        resultField.setEditable(false);
        add(resultField);

        pack();
        setSize(800,400);
        setLocationRelativeTo(null);
    }

    private void convertTemperature() {
        try {
            double inputTemperature = Double.parseDouble(inputField.getText());

            if (celsiusRadio.isSelected()) {
                resultField.setText(convertCelsiusToFahrenheit(inputTemperature) + " °F / "
                        + convertCelsiusToKelvin(inputTemperature) + " K");
            } else if (fahrenheitRadio.isSelected()) {
                resultField.setText(convertFahrenheitToCelsius(inputTemperature) + " °C / "
                        + convertFahrenheitToKelvin(inputTemperature) + " K");
            } else if (kelvinRadio.isSelected()) {
                resultField.setText(convertKelvinToCelsius(inputTemperature) + " °C / "
                        + convertKelvinToFahrenheit(inputTemperature) + " °F");
            }
        } catch (NumberFormatException ex) {
            JOptionPane.showMessageDialog(this, "Invalid input. Please enter a valid temperature.", "Error", JOptionPane.ERROR_MESSAGE);
        }
    }

    private double convertCelsiusToFahrenheit(double celsius) {
        return (celsius * 9 / 5) + 32;
    }

    private double convertCelsiusToKelvin(double celsius) {
        return celsius + 273.15;
    }

    private double convertFahrenheitToCelsius(double fahrenheit) {
        return (fahrenheit - 32) * 5 / 9;
    }

    private double convertFahrenheitToKelvin(double fahrenheit) {
        return (fahrenheit + 459.67) * 5 / 9;
    }

    private double convertKelvinToCelsius(double kelvin) {
        return kelvin - 273.15;
    }

    private double convertKelvinToFahrenheit(double kelvin) {
        return (kelvin * 9 / 5) - 459.67;
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
            @Override
            public void run() {
                new TemperatureConverter().setVisible(true);
            }
        });
    }
}
