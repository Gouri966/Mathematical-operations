# Mathematical-operations
GUI Calci
<br>
graphical calculator using java
<br>
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class Calculator extends JFrame implements ActionListener {

    JTextField textField;
    JButton[] numberButtons = new JButton[10];
    JButton[] functionButtons = new JButton[10];

    JButton addButton, subButton, mulButton, divButton;
    JButton decButton, equButton, delButton, clrButton;
    JButton negButton, modButton;

    JPanel panel;

    Font myFont = new Font("Arial", Font.BOLD, 22);

    double num1 = 0, num2 = 0, result = 0;
    char operator;

    Calculator() {

        setTitle("Java Swing Calculator");
        setSize(420, 550);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(null);
        setLocationRelativeTo(null);

        textField = new JTextField();
        textField.setBounds(30, 25, 340, 50);
        textField.setFont(myFont);
        textField.setEditable(false);
        textField.setHorizontalAlignment(JTextField.RIGHT);

        add(textField);

        addButton = new JButton("+");
        subButton = new JButton("-");
        mulButton = new JButton("*");
        divButton = new JButton("/");
        decButton = new JButton(".");
        equButton = new JButton("=");
        delButton = new JButton("Del");
        clrButton = new JButton("Clear");
        negButton = new JButton("+/-");
        modButton = new JButton("%");

        functionButtons[0] = addButton;
        functionButtons[1] = subButton;
        functionButtons[2] = mulButton;
        functionButtons[3] = divButton;
        functionButtons[4] = decButton;
        functionButtons[5] = equButton;
        functionButtons[6] = delButton;
        functionButtons[7] = clrButton;
        functionButtons[8] = negButton;
        functionButtons[9] = modButton;

        for (JButton button : functionButtons) {
            button.addActionListener(this);
            button.setFont(myFont);
            button.setFocusable(false);
        }

        for (int i = 0; i < 10; i++) {
            numberButtons[i] = new JButton(String.valueOf(i));
            numberButtons[i].addActionListener(this);
            numberButtons[i].setFont(myFont);
            numberButtons[i].setFocusable(false);
        }

        negButton.setBounds(30, 90, 100, 40);
        delButton.setBounds(140, 90, 100, 40);
        clrButton.setBounds(250, 90, 120, 40);

        add(negButton);
        add(delButton);
        add(clrButton);

        panel = new JPanel();
        panel.setBounds(30, 150, 340, 300);
        panel.setLayout(new GridLayout(4, 4, 10, 10));

        panel.add(numberButtons[1]);
        panel.add(numberButtons[2]);
        panel.add(numberButtons[3]);
        panel.add(addButton);

        panel.add(numberButtons[4]);
        panel.add(numberButtons[5]);
        panel.add(numberButtons[6]);
        panel.add(subButton);

        panel.add(numberButtons[7]);
        panel.add(numberButtons[8]);
        panel.add(numberButtons[9]);
        panel.add(mulButton);

        panel.add(decButton);
        panel.add(numberButtons[0]);
        panel.add(equButton);
        panel.add(divButton);

        add(panel);

        modButton.setBounds(30, 460, 340, 40);
        add(modButton);

        setVisible(true);
    }

    public void actionPerformed(ActionEvent e) {

        for (int i = 0; i < 10; i++) {
            if (e.getSource() == numberButtons[i]) {
                textField.setText(textField.getText().concat(String.valueOf(i)));
            }
        }

        if (e.getSource() == decButton) {
            if (!textField.getText().contains(".")) {
                textField.setText(textField.getText() + ".");
            }
        }

        if (e.getSource() == addButton) {
            num1 = Double.parseDouble(textField.getText());
            operator = '+';
            textField.setText("");
        }

        if (e.getSource() == subButton) {
            num1 = Double.parseDouble(textField.getText());
            operator = '-';
            textField.setText("");
        }

        if (e.getSource() == mulButton) {
            num1 = Double.parseDouble(textField.getText());
            operator = '*';
            textField.setText("");
        }

        if (e.getSource() == divButton) {
            num1 = Double.parseDouble(textField.getText());
            operator = '/';
            textField.setText("");
        }

        if (e.getSource() == modButton) {
            num1 = Double.parseDouble(textField.getText());
            operator = '%';
            textField.setText("");
        }

        if (e.getSource() == equButton) { 

            num2 = Double.parseDouble(textField.getText());

            switch (operator) {

                case '+':
                    result = num1 + num2;
                    break;

                case '-':
                    result = num1 - num2;
                    break;

                case '*':
                    result = num1 * num2;
                    break;

                case '/':
                    if (num2 == 0) {
                        JOptionPane.showMessageDialog(this,
                                "Cannot divide by zero!");
                        return;
                    }
                    result = num1 / num2;
                    break;

                case '%':
                    result = num1 % num2;
                    break;
            }

            textField.setText(String.valueOf(result));
            num1 = result;
        }

        if (e.getSource() == clrButton) {
            textField.setText("");
            num1 = 0;
            num2 = 0;
        }

        if (e.getSource() == delButton) {

            String str = textField.getText();

            if (!str.isEmpty()) {
                textField.setText(str.substring(0, str.length() - 1));
            }
        }

        if (e.getSource() == negButton) {

            if (!textField.getText().isEmpty()) {

                double temp = Double.parseDouble(textField.getText());
                temp *= -1;
                textField.setText(String.valueOf(temp));
            }
        }
    }

    public static void main(String[] args) {

        SwingUtilities.invokeLater(() -> new Calculator());

    }
}
