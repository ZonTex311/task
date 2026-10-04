import java.util.*;

class Telebe {
    String ad;
    String soyad;
    int yas;
    String fakulte;
    String id;
    Integer qiymet;

    Telebe(String ad, String soyad, int yas, String fakulte, String id) {
        this.ad = ad;
        this.soyad = soyad;
        this.yas = yas;
        this.fakulte = fakulte;
        this.id = id;
        this.qiymet = null;
    }
}

public class Main {
    static List<Telebe> telebeler = new ArrayList<>();
    static Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        while (true) {
            System.out.println("\n1 - Telebeler daxil et");
            System.out.println("2 - Telebelerin axtar");
            System.out.println("3 - Telebelerin qiymet daxil");
            System.out.println("0 - Cixis");
            System.out.print("Seciminizi edin: ");

            int secim;
            try {
                secim = Integer.parseInt(scanner.nextLine().trim());
            } catch (NumberFormatException e) {
                System.out.println("Zehmet olmasa reqem daxil edin!");
                continue;
            }

            switch (secim) {
                case 1: telebeDaxilEt();
                    break;
                case 2: telebeleriGoster();
                    break;
                case 3: qiymetDaxilEt();
                    break;
                case 0: System.out.println("Cixis edilir...");
                    return;
                default: System.out.println("Yanlis secim! Yeniden cehd edin.");
            }
        }
    }


    static void telebeDaxilEt() {
        System.out.print("Ad: ");
        String ad = scanner.nextLine().trim();

        System.out.print("Soyad: ");
        String soyad = scanner.nextLine().trim();

        int yas;
        while (true) {
            System.out.print("Yas: ");
            try {
                yas = Integer.parseInt(scanner.nextLine().trim());
            } catch (NumberFormatException e) {
                System.out.println("Zehmet olmasa reqem daxil edin!");
                continue;
            }

            if (yas < 6) {
                System.out.println("Xeta: 6 yasdan kicik telebe qeydiyyatdan kecire bilmez!");
            } else if (yas > 100) {
                System.out.println("Xeta: 100 yasdan boyuk telebe qeydiyyatdan kecire bilmez!");
            } else {
                break;
            }
        }

        System.out.print("Fakulte: ");
        String fakulte = scanner.nextLine().trim();

        System.out.print("ID/FIN kod: ");
        String id = scanner.nextLine().trim();

        Telebe yeni = new Telebe(ad, soyad, yas, fakulte, id);
        telebeler.add(yeni);
        System.out.println("Telebe ugurla elave edildi!");
    }


    static void telebeleriGoster() {
        if (telebeler.isEmpty()) {
            System.out.println("Hec bir telebe qeyde alinmayib.");
            return;
        }

        for (Telebe t : telebeler) {
            System.out.println("-------------------");
            System.out.println("Ad Soyad: " + t.ad + " " + t.soyad);
            System.out.println("Fakulte: " + t.fakulte);
            System.out.println("Qiymet: " + (t.qiymet == null ? "Hele daxil edilmeyib" : t.qiymet));
        }
        System.out.println("-------------------");
    }



    static void qiymetDaxilEt() {
        if (telebeler.isEmpty()) {
            System.out.println("Hec bir telebe qeyde alinmayib.");
            return;
        }

        System.out.print("ID/FIN kod daxil edin: ");
        String id = scanner.nextLine().trim();

        Telebe tapilan = null;
        for (Telebe t : telebeler) {
            if (t.id.equals(id)) {
                tapilan = t;
                break;
            }
        }

        if (tapilan == null) {
            System.out.println("Bu ID/FIN koduna uygun telebe tapilmadi!");
            return;
        }

        int qiymet;
        while (true) {
            System.out.print("Qiymeti daxil edin (0-100): ");
            try {
                qiymet = Integer.parseInt(scanner.nextLine().trim());
            } catch (NumberFormatException e) {
                System.out.println("Zehmet olmasa reqem daxil edin!");
                continue;
            }

            if (qiymet < 0 || qiymet > 100) {
                System.out.println("Xeta: qiymet 0 ile 100 arasinda olmalidir!");
            } else {
                break;
            }
        }

        tapilan.qiymet = qiymet;
        System.out.println("Qiymet " + tapilan.ad + " " + tapilan.soyad + " ucun elave edildi!");

    }
}
