package com.company;
import java.util.*;

public class Main {

    public static void main(String[] args) {

        Scanner in = new Scanner(System.in);

        System.out.println("Введите количество переменных");
        String aaa = in.nextLine();

        Strokaa obj = new Strokaa(aaa);
        int cl = obj.razbienie();

        int[] aa = new int[2];

        if (cl == 3)
            obj.proverka();
    }

}





package com.company;

public class Strokaa {

    private String[] slovo = new String[3]; // неточность

    private int cl = 0;//количество слов в строке
    private int n;
    private String ss;
    private char c = 'q';

    public Strokaa(String ll) {
        ss = ll;
        n = ss.length();
    }

    public int razbienie() {
        ss = ss + " ";

        for (int i = 1; i <= n; i++) {
            c = ss.charAt(i);//выделение символов

            if ((c == ' ') && (ss.charAt(i - 1) != ' '))
                cl++;
        }

        int l = 0;
        if (cl == 3) {

            for (int i = 0; i < 3; i++) {
                slovo[i] = "";
            }

            for (int i = 1; i <= n; i++) {
                c = ss.charAt(i);//выделение символов

                if (ss.charAt(i - 1) != ' ')
                    slovo[l] = slovo[l] + ss.charAt(i - 1);

                if ((c == ' ') && (ss.charAt(i - 1) != ' '))
                    l++;
            }
        }
        return cl;
    }

    public void proverka() {//проверка на соответствие цифрам(араб и рим)

        String[] arab = new String[]{"1", "2", "3", "4", "5", "6", "7", "8", "9", "10"};
        String[] rim = new String[]{"I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX", "X"};
        String[] opera = new String[]{"+", "-", "*", "/"};

        int[] aa = new int[2];

        for (int j = 0; j < 10; j++) {
            if (slovo[0].equals(arab[j]))
                ++aa[0];
            if (slovo[2].equals(arab[j]))
                ++aa[0];
        }
        for (int j = 0; j < 4; j++) {
            if (slovo[1].equals(opera[j]))
                ++aa[0];
        }

        for (int j = 0; j < 10; j++) {
            if (slovo[0].equals(rim[j]))
                ++aa[1];
            if (slovo[2].equals(rim[j]))
                ++aa[1];
        }
        for (int j = 0; j < 4; j++) {
            if (slovo[1].equals(opera[j]))
                ++aa[1];
        }

        if (aa[0] == 3) {
            Operacia wq = new Operacia(slovo);
            wq.perevod_arab();
            int result = wq.vichisl();
            System.out.println(result);
        }
        if (aa[1] == 3) {
            Operacia wq = new Operacia(slovo);
            int l = wq.perevod_rim();
            if (!((l == 0)&&(slovo[1].equals(opera[1])))) {//если не(< и -)
                wq.vichisl();
                String result = wq.result_rim();
                System.out.println(result);
            }

        }

    }
}






package com.company;

public class Operacia {
    private int lol;
    private String[] ss;
    private int result;
    int[] sl = new int[3];

    public Operacia(String[] slovo){
        ss = slovo;
    }

    public int perevod_rim(){

        String[] rim = new String[]{"I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX", "X"};

        for (int j = 0; j < 10; j++) {
            if (ss[0].equals(rim[j]))
                sl[0] = j+1;
            if (ss[2].equals(rim[j]))
                sl[2] = j+1;
        }
        if (sl[0]<=sl[2])
            return 0;
        else
            return 1;
    }

    public void perevod_arab(){
        String[] arab = new String[]{"1", "2", "3", "4", "5", "6", "7", "8", "9", "10"};

        for (int j = 0; j < 10; j++) {
            if (ss[0].equals(arab[j]))
                sl[0] = j+1;
            if (ss[2].equals(arab[j]))
                sl[2] = j+1;
        }
    }

    public int vichisl(){
        String[] opera = new String[]{"+", "-", "*", "/"};

        if (ss[1].equals(opera[0]))
            result = sl[0] + sl[2];
        if (ss[1].equals(opera[1]))
            result = sl[0] - sl[2];
        if (ss[1].equals(opera[2]))
            result = sl[0] * sl[2];
        if (ss[1].equals(opera[3]))
            result = sl[0] / sl[2];

        return result;
    }

    public String result_rim(){
        String[] rim = new String[]{"I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX", "X"};
        String[] rimd = new String[]{"X","XX","XXX","XL","L","LX","LXX","LXXX","XC","C"};

        String rr;
        String po = "";
        String vo = "";
        int l = result;
        int k = 0;

        while(l>0) {
            k++;
            l /= 10;
        }

        if ((k==2)||(k==3)) {
            int nn = result / 10;
            int ww = result % 10;

            for (int j = 0; j < 10; j++) {
                if (nn == j+1)
                    po = rimd[j];
                if (ww == j+1)
                    vo = rim[j];
            }
            po = po + vo;
        }

        if (k==1){
            for (int j = 0; j < 10; j++) {
                if (result == j+1)
                    po = rim[j];
            }
        }
        return po;
    }
}








