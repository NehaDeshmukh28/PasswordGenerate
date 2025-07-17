# PasswordGenerate
#Level-1 Task-3
import javax.swing.*;
import java.awt.event.*;
import java.util.Random;

public class PasswordGenerator extends JFrame {
    private JTextField lengthField;
    private final JCheckBox includeLowercase;
    private final JCheckBox includeUppercase;
    private final JCheckBox includeNumbers;
    private final JCheckBox includeSymbols;
    private final JButton generateButton;
    private JLabel resultLabel;

    public PasswordGenerator() {
        setTitle("Random Password Generator");
        setSize(400, 300);
        setLayout(null);
        setDefaultCloseOperation(EXIT_ON_CLOSE);

        JLabel lengthLabel = new JLabel("Password Length:");
        lengthLabel.setBounds(30, 20, 120, 30);
        add(lengthLabel);

        lengthField = new JTextField();
        lengthField.setBounds(160, 20, 50, 30);
        add(lengthField);

        includeLowercase = new JCheckBox("Include Lowercase");
        includeLowercase.setBounds(30, 60, 200, 30);
        add(includeLowercase);

        includeUppercase = new JCheckBox("Include Uppercase");
        includeUppercase.setBounds(30, 90, 200, 30);
        add(includeUppercase);

        includeNumbers = new JCheckBox("Include Numbers");
        includeNumbers.setBounds(30, 120, 200, 30);
        add(includeNumbers);

        includeSymbols = new JCheckBox("Include Symbols");
        includeSymbols.setBounds(30, 150, 200, 30);
        add(includeSymbols);

        generateButton = new JButton("Generate Password");
        generateButton.setBounds(100, 190, 180, 30);
        add(generateButton);

        resultLabel = new JLabel("Generated Password: ");
        resultLabel.setBounds(30, 230, 340, 30);
        add(resultLabel);

        generateButton.addActionListener((ActionEvent e) -> {
            try {
                int length = Integer.parseInt(lengthField.getText());
                String password = generatePassword(length);
                resultLabel.setText("Password: " + password);
            } catch (NumberFormatException ex) {
                JOptionPane.showMessageDialog(null, "Enter a valid number for length!");
            }
        });

        setVisible(true);
    }

    private String generatePassword(int length) {
        String lower = "abcdefghijklmnopqrstuvwxyz";
        String upper = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
        String numbers = "0123456789";
        String symbols = "!@#$%^&*()-_=+[]{}|;:'\",.<>?/";

        StringBuilder characterSet = new StringBuilder();

        if (includeLowercase.isSelected()) characterSet.append(lower);
        if (includeUppercase.isSelected()) characterSet.append(upper);
        if (includeNumbers.isSelected()) characterSet.append(numbers);
        if (includeSymbols.isSelected()) characterSet.append(symbols);

        if (characterSet.length() == 0) return "Please select at least one option.";

        Random rand = new Random();
        StringBuilder password = new StringBuilder();

        for (int i = 0; i < length; i++) {
            int index = rand.nextInt(characterSet.length());
            password.append(characterSet.charAt(index));
        }

        return password.toString();
    }

    public static void main(String[] args) {
        new PasswordGenerator(); // Launch GUI
    }
}
