import java.awt.*;
import java.awt.event.*;
import java.awt.geom.Ellipse2D;
import javax.swing.BorderFactory;
import javax.swing.JButton;


public class MyCalculator extends Frame{

    public boolean setClear=true;
    double number, memValue;
    char op;

    String digitButtonText[] = {"7", "8", "9", "4", "5", "6", "1", "2", "3", "0", "+/-", "." };
    String operatorButtonText[] = {"/", "sqrt", "*", "%", "-", "1/X", "+", "=" };
    String memoryButtonText[] = {"MC", "MR", "MS", "M+" };
    String specialButtonText[] = {"Backspc", "C", "CE" };

    MyDigitButton digitButton[]=new MyDigitButton[digitButtonText.length];
    MyOperatorButton operatorButton[]=new MyOperatorButton[operatorButtonText.length];
    MyMemoryButton memoryButton[]=new MyMemoryButton[memoryButtonText.length];
    MySpecialButton specialButton[]=new MySpecialButton[specialButtonText.length];

    Label displayLabel=new Label("0",Label.RIGHT);
    Label memLabel=new Label(" ",Label.RIGHT);

    final int FRAME_WIDTH=325,FRAME_HEIGHT=325;
    final int HEIGHT=30, WIDTH=30, H_SPACE=10,V_SPACE=10;
    final int TOPX=30, TOPY=50;
    ///////////////////////////
    MyCalculator(String frameText){
        super(frameText);

        int tempX=TOPX, y=TOPY;
        displayLabel.setBounds(tempX,y,240,HEIGHT);
        displayLabel.setBackground(Color.BLACK); // Ubah warna latar belakang menjadi hitam
        displayLabel.setForeground(Color.WHITE);
        add(displayLabel);

        memLabel.setBounds(TOPX,  TOPY+HEIGHT+ V_SPACE,WIDTH, HEIGHT);
        add(memLabel);

// set Co-ordinates for Memory Buttons
        tempX=TOPX;
        y=TOPY+2*(HEIGHT+V_SPACE);
        for(int i=0; i<memoryButton.length; i++){
            memoryButton[i]=new MyMemoryButton(tempX,y,WIDTH,HEIGHT,memoryButtonText[i], this);
            memoryButton[i].setForeground(Color.WHITE);
            y+=HEIGHT+V_SPACE;
        }

//set Co-ordinates for Special Buttons
        tempX=TOPX+1*(WIDTH+H_SPACE); y=TOPY+1*(HEIGHT+V_SPACE);
        for(int i=0;i<specialButton.length;i++){
            specialButton[i]=new MySpecialButton(tempX,y,WIDTH*2,HEIGHT,specialButtonText[i], this);
            specialButton[i].setForeground(Color.BLACK);
            tempX=tempX+2*WIDTH+H_SPACE;
        }

//set Co-ordinates for Digit Buttons
        int digitX=TOPX+WIDTH+H_SPACE;
        int digitY=TOPY+2*(HEIGHT+V_SPACE);
        tempX=digitX;  y=digitY;
        for(int i=0;i<digitButton.length;i++){
            digitButton[i]=new MyDigitButton(tempX,y,WIDTH,HEIGHT,digitButtonText[i], this);
            digitButton[i].setForeground(Color.WHITE);
            tempX+=WIDTH+H_SPACE;
            if((i+1)%3==0){tempX=digitX; y+=HEIGHT+V_SPACE;}
        }

//set Co-ordinates for Operator Buttons
        int opsX = digitX + 2 * (WIDTH + H_SPACE) + H_SPACE;
        int opsY = digitY;
        tempX = opsX;
        y = opsY;
        for (int i = 0; i < operatorButton.length; i++) {
            tempX += WIDTH + H_SPACE;
            operatorButton[i] = new MyOperatorButton(tempX, y, WIDTH, HEIGHT, operatorButtonText[i], this);
            operatorButton[i].setForeground(Color.WHITE);
            if ((i + 1) % 2 == 0) {
                tempX = opsX;
                y += HEIGHT + V_SPACE;
            }
        }


        addWindowListener(new WindowAdapter(){
            public void windowClosing(WindowEvent ev)
            {System.exit(0);}
        });

        setLayout(null);
        setBackground(Color.BLACK); // Ubah warna latar belakang frame menjadi hitam
        setSize(FRAME_WIDTH,FRAME_HEIGHT);
        setVisible(true);
    }
    //////////////////////////////////
    static String getFormattedText(double temp){
        String resText=""+temp;
        if(resText.lastIndexOf(".0")>0)
            resText=resText.substring(0,resText.length()-2);
        return resText;
    }
    ////////////////////////////////////////
    public static void main(String []args){
        new MyCalculator("Calculator - JavaTpoint - Noval083");
    }
}

/*******************************************/

class MyDigitButton extends JButton implements ActionListener {
    MyCalculator cl;

    MyDigitButton(int x, int y, int diameter, int height, String cap, MyCalculator clc) {
        super(cap);
        setBounds(x, y, diameter, diameter);
        setBackground(new Color(88, 88, 88));
        this.cl = clc;
        this.cl.add(this);
        addActionListener(this);

        // Set an empty border
        setBorder(BorderFactory.createEmptyBorder());
    }

    public void actionPerformed(ActionEvent ev) {
        String tempText = ((MyDigitButton) ev.getSource()).getLabel();

        // Mengembalikan warna dan status tombol memori ke kondisi awal
        for (MyMemoryButton memoryButton : cl.memoryButton) {
            memoryButton.setBackground(new Color(248, 152, 32));
            memoryButton.setForeground(Color.WHITE);
        }

        // Mengembalikan warna dan status tombol operator ke kondisi awal
        for (MyOperatorButton operatorButton : cl.operatorButton) {
            operatorButton.setBackground(new Color(248, 152, 32));
            operatorButton.setForeground(Color.WHITE);
        }

        if (tempText.equals(".")) {
            if (cl.setClear) {
                cl.displayLabel.setText("0.");
                cl.setClear = false;
            } else if (!isInString(cl.displayLabel.getText(), '.')) {
                cl.displayLabel.setText(cl.displayLabel.getText() + ".");
            }
            return;
        }

        int index = 0;
        try {
            index = Integer.parseInt(tempText);
        } catch (NumberFormatException e) {
            return;
        }

        if (index == 0 && cl.displayLabel.getText().equals("0")) return;

        if (cl.setClear) {
            cl.displayLabel.setText("" + index);
            cl.setClear = false;
        } else
            cl.displayLabel.setText(cl.displayLabel.getText() + index);
    }

    static boolean isInString(String s, char ch) {
        for (int i = 0; i < s.length(); i++) if (s.charAt(i) == ch) return true;
        return false;
    }

    @Override
    public void paint(Graphics g) {
        Graphics2D g2d = (Graphics2D) g;
        g2d.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);

        Ellipse2D.Double circle = new Ellipse2D.Double(0, 0, getWidth() - 1, getHeight() - 1);
        g2d.setColor(getBackground());
        g2d.fill(circle);

        FontMetrics fm = g.getFontMetrics();
        int x = (getWidth() - fm.stringWidth(getLabel())) / 2;
        int y = (getHeight() + fm.getHeight()) / 2 - 2;

        g2d.setColor(getForeground());
        g2d.drawString(getLabel(), x, y);
    }
}


class MyOperatorButton extends JButton implements ActionListener {
    MyCalculator cl;
    boolean isActive = false; // Tambahkan variabel status

    MyOperatorButton(int x, int y, int diameter, int height, String cap, MyCalculator clc) {
        super(cap);
        setBounds(x, y, diameter, diameter);
        setBackground(new Color(248, 152, 32));
        this.cl = clc;
        this.cl.add(this);
        addActionListener(this);

        // Set an empty border
        setBorder(BorderFactory.createEmptyBorder());
    }

    public void actionPerformed(ActionEvent ev) {
        String opText = ((MyOperatorButton) ev.getSource()).getLabel();

        // Atur warna dan status ketika operator dipilih
        if (!isActive) {
            setBackground(Color.WHITE);
            setForeground(new Color(248, 152, 32));
            isActive = true;
        }

        cl.setClear = true;
        double temp = Double.parseDouble(cl.displayLabel.getText());

        if (opText.equals("1/x")) {
            try {
                double tempd = 1 / (double) temp;
                cl.displayLabel.setText(MyCalculator.getFormattedText(tempd));
            } catch (ArithmeticException excp) {
                cl.displayLabel.setText("Divide by 0.");
            }
            return;
        }
        if (opText.equals("sqrt")) {
            try {
                double tempd = Math.sqrt(temp);
                cl.displayLabel.setText(MyCalculator.getFormattedText(tempd));
            } catch (ArithmeticException excp) {
                cl.displayLabel.setText("Divide by 0.");
            }
            return;
        }
        if (!opText.equals("=")) {
            cl.number = temp;
            cl.op = opText.charAt(0);
            return;
        }

        // Atur warna dan status ketika operator selesai diaktifkan
        if (isActive) {
            setBackground(new Color(248, 152, 32));
            setForeground(Color.WHITE);
            isActive = false;
        }

        // proses tombol = ditekan
        switch (cl.op) {
            case '+':
                temp += cl.number;
                break;
            case '-':
                temp = cl.number - temp;
                break;
            case '*':
                temp *= cl.number;
                break;
            case '%':
                try {
                    temp = cl.number % temp;
                } catch (ArithmeticException excp) {
                    cl.displayLabel.setText("Divide by 0.");
                    return;
                }
                break;
            case '/':
                try {
                    temp = cl.number / temp;
                } catch (ArithmeticException excp) {
                    cl.displayLabel.setText("Divide by 0.");
                    return;
                }
                break;
        }//switch

        cl.displayLabel.setText(MyCalculator.getFormattedText(temp));
    }//actionPerformed

    @Override
    public void paint(Graphics g) {
        Graphics2D g2d = (Graphics2D) g;
        g2d.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);

        Ellipse2D.Double circle = new Ellipse2D.Double(0, 0, getWidth() - 1, getHeight() - 1);
        g2d.setColor(getBackground());
        g2d.fill(circle);

        FontMetrics fm = g.getFontMetrics();
        int x = (getWidth() - fm.stringWidth(getLabel())) / 2;
        int y = (getHeight() + fm.getHeight()) / 2 - 2;

        g2d.setColor(getForeground());
        g2d.drawString(getLabel(), x, y);
    }
}


class MyMemoryButton extends JButton implements ActionListener {
    MyCalculator cl;

    MyMemoryButton(int x, int y, int width, int height, String cap, MyCalculator clc) {
        super(cap);
        setBounds(x, y, width, height);
        setBackground(new Color(248, 152, 32));
        this.cl = clc;
        this.cl.add(this);
        addActionListener(this);

        // Set an empty border
        setBorder(BorderFactory.createEmptyBorder());
    }

    public void actionPerformed(ActionEvent ev) {
        char memop = ((MyMemoryButton) ev.getSource()).getLabel().charAt(1);

        cl.setClear = true;
        double temp = Double.parseDouble(cl.displayLabel.getText());

        switch (memop) {
            case 'C':
                cl.memLabel.setText(" ");
                cl.memValue = 0.0;
                break;
            case 'R':
                cl.displayLabel.setText(MyCalculator.getFormattedText(cl.memValue));
                break;
            case 'S':
                cl.memValue = 0.0;
            case '+':
                cl.memValue += Double.parseDouble(cl.displayLabel.getText());
                if (cl.displayLabel.getText().equals("0") || cl.displayLabel.getText().equals("0.0"))
                    cl.memLabel.setText(" ");
                else
                    cl.memLabel.setText("M");
                break;
        }//switch
    }//actionPerformed

    @Override
    public void paint(Graphics g) {
        Graphics2D g2d = (Graphics2D) g;
        g2d.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);

        Ellipse2D.Double circle = new Ellipse2D.Double(0, 0, getWidth() - 1, getHeight() - 1);
        g2d.setColor(getBackground());
        g2d.fill(circle);

        FontMetrics fm = g.getFontMetrics();
        int x = (getWidth() - fm.stringWidth(getLabel())) / 2;
        int y = (getHeight() + fm.getHeight()) / 2 - 2;

        g2d.setColor(getForeground());
        g2d.drawString(getLabel(), x, y);
    }
}

class MySpecialButton extends JButton implements ActionListener {
    MyCalculator cl;

    MySpecialButton(int x, int y, int width, int height, String cap, MyCalculator clc) {
        super(cap);
        setBounds(x, y, width, height);
        setBackground(new Color(224, 224, 224));
        this.cl = clc;
        this.cl.add(this);
        addActionListener(this);

        // Set an empty border
        setBorder(BorderFactory.createEmptyBorder());
    }

    static String backSpace(String s) {
        String Res = "";
        for (int i = 0; i < s.length() - 1; i++) Res += s.charAt(i);
        return Res;
    }

    public void actionPerformed(ActionEvent ev) {
        String opText = ((MySpecialButton) ev.getSource()).getLabel();

        // Mengembalikan warna dan status operator ke kondisi awal
        for (MyOperatorButton operatorButton : cl.operatorButton) {
            if (operatorButton.isActive) {
                operatorButton.setBackground(new Color(248, 152, 32));
                operatorButton.setForeground(Color.WHITE);
                operatorButton.isActive = false;
            }
        }

        // cek untuk tombol "Backspc"
        if (opText.equals("Backspc")) {
            String tempText = backSpace(cl.displayLabel.getText());
            if (tempText.equals(""))
                cl.displayLabel.setText("0");
            else
                cl.displayLabel.setText(tempText);
            return;
        }

        // cek untuk tombol "C"
        if (opText.equals("C")) {
            cl.number = 0.0;
            cl.op = ' ';
            cl.memValue = 0.0;
            cl.memLabel.setText(" ");
        }

        // itu harus menjadi tombol CE yang ditekan
        cl.displayLabel.setText("0");
        cl.setClear = true;
    }//actionPerformed

    @Override
    public void paint(Graphics g) {
        Graphics2D g2d = (Graphics2D) g;
        g2d.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);

        if (getLabel().equals("Backspc")) {
            // Gambar oval untuk tombol Backspc
            Ellipse2D.Double oval = new Ellipse2D.Double(0, 0, getWidth() - 1, getHeight() - 1);
            g2d.setColor(getBackground());
            g2d.fill(oval);
        } else {
            // Gambar persegi panjang untuk tombol "C" dan "CE"
            g2d.setColor(getBackground());
            g2d.fillRect(0, 0, getWidth() - 1, getHeight() - 1);
        }

        FontMetrics fm = g.getFontMetrics();
        int x = (getWidth() - fm.stringWidth(getLabel())) / 2;
        int y = (getHeight() + fm.getHeight()) / 2 - 2;


        g2d.setColor(getForeground());
        g2d.drawString(getLabel(), x, y);
    }
}
