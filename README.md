import javax.swing.*;

import java.awt.*;

import java.awt.event.*;



 class SimpleCalculator extends JFrame implements ActionListener {

    private JTextField tf;

    private JButton[] numBtns = new JButton[10];

    private JButton add, sub, mul, div, eq, clr;

    private double first = 0, second = 0;

    private String op = "";



    public SimpleCalculator() {

        setTitle("Simple Calculator");

        setSize(320, 420);

        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        setLocationRelativeTo(null);



        tf = new JTextField();

        tf.setEditable(false);

        tf.setHorizontalAlignment(JTextField.RIGHT);



        JPanel panel = new JPanel();

        panel.setLayout(new GridLayout(4, 4, 5, 5));



        for (int i = 1; i <= 9; i++) {

            numBtns[i] = new JButton(String.valueOf(i));

            numBtns[i].addActionListener(this);

        }

        numBtns[0] = new JButton("0"); numBtns[0].addActionListener(this);



        add = new JButton("+"); sub = new JButton("-"); mul = new JButton("*"); div = new JButton("/");

        eq = new JButton("="); clr = new JButton("C");



        add.addActionListener(this);

        sub.addActionListener(this);

        mul.addActionListener(this);

        div.addActionListener(this);

        eq.addActionListener(this);

        clr.addActionListener(this);



        // Add components: simple layout

        getContentPane().setLayout(new BorderLayout(5,5));

        getContentPane().add(tf, BorderLayout.NORTH);



        panel.add(numBtns[7]); panel.add(numBtns[8]); panel.add(numBtns[9]); panel.add(div);

        panel.add(numBtns[4]); panel.add(numBtns[5]); panel.add(numBtns[6]); panel.add(mul);

        panel.add(numBtns[1]); panel.add(numBtns[2]); panel.add(numBtns[3]); panel.add(sub);

        panel.add(numBtns[0]); panel.add(clr); panel.add(eq); panel.add(add);



        getContentPane().add(panel, BorderLayout.CENTER);

    }



    @Override

    public void actionPerformed(ActionEvent e) {

        Object src = e.getSource();

        for (int i = 0; i <= 9; i++) if (src == numBtns[i]) {

            tf.setText(tf.getText() + i);

            return;

        }

        if (src == clr) {

            tf.setText("");

            first = second = 0;

            op = "";

            return;

        }

        if (src == add || src == sub || src == mul || src == div) {

            try {

                first = Double.parseDouble(tf.getText());

            } catch (NumberFormatException ex) { first = 0; }

            op = ((JButton)src).getText();

            tf.setText("");

            return;

        }

        if (src == eq) {

            try {

                second = Double.parseDouble(tf.getText());

            } catch (NumberFormatException ex) { second = 0; }

            double res = 0;

            switch (op) {

                case "+": res = first + second; break;

                case "-": res = first - second; break;

                case "*": res = first * second; break;

                case "/":

                    if (second == 0) { tf.setText("Error: Div by 0"); return; }

                    res = first / second; break;

                default: res = second;

            }

            tf.setText(String.valueOf(res));

            op = "";

            first = res;

        }

    }



    public static void main(String[] args) {

        SwingUtilities.invokeLater(() -> {

            SimpleCalculator calc = new SimpleCalculator();

            calc.setVisible(true);

        });

    }

}
