#include <stdio.h>

#define MAX 100

struct Item {
    char nama[50];
    int harga;
};

// Daftar buku
struct Item daftarBuku[] = {
    {"Novel Laskar Pelangi", 85000},
    {"Buku Fisika", 65000},
    {"Buku Biologi", 60000},
    {"Buku Sejarah Dunia", 70000},
    {"Novel Dilan 1990", 80000},
    {"Komik One Piece Vol.1", 55000},
    {"Komik Naruto Vol.1", 50000},
    {"Ensiklopedia Sains", 95000},
    {"Novel Your Name", 60000},
    {"Buku Matematika", 65000}
};

// Daftar alat tulis
struct Item daftarAlatTulis[] = {
    {"Pulpen Hitam", 3000},
    {"Pensil 2B", 2000},
    {"Buku Tulis 58 Lembar", 8000},
    {"Penghapus", 3000},
    {"Penggaris 30cm", 5000},
    {"Spidol Boardmarker", 10000},
    {"Highlighter", 12000},
    {"Stabilo Warna", 15000},
    {"Tempat Pensil", 20000},
    {"Tas", 95000}
};

int main() {
    printf("=====================================================\n");
    printf("          SELAMAT DATANG DI TOKO BUKU                \n");
    printf("=====================================================\n\n");
    printf("      ___________________________________________\n");
    printf("     |                                           |\n");
    printf("     |               [ TOKO BUKU ]               |\n");
    printf("     |___________________________________________|\n");
    printf("                   Buku, Alat Tulis               \n");
    printf("=====================================================\n\n");

    int jumlahBuku = sizeof(daftarBuku) / sizeof(daftarBuku[0]);
    int jumlahAlatTulis = sizeof(daftarAlatTulis) / sizeof(daftarAlatTulis[0]);

    int pilihanBuku[MAX], jumlahBukuArr[MAX];
    int pilihanAlatTulis[MAX], jumlahAlatTulisArr[MAX];
    int total = 0, bayar, kembalian;
    char lanjut;
    int iBuku = 0, iAlat = 0;
    float diskon = 0.0;
    int member = 0;

    char namaPembeli[50];
    printf("Masukkan nama pembeli: ");
    scanf(" %[^\n]", namaPembeli);

    printf("Apakah Anda memiliki kartu member? (y/n): ");
    scanf(" %c", &lanjut);
    if (lanjut == 'y' || lanjut == 'Y') {
        member = 1;
        printf("Anda mendapat diskon tambahan 5%%.\n");
    }

    printf("\n=== DAFTAR BUKU ===\n");
    for (int j = 0; j < jumlahBuku; j++) {
        printf("%2d. %-25s - Rp%d\n", j + 1, daftarBuku[j].nama, daftarBuku[j].harga);
    }

    printf("\nBeli buku? (y/n): ");
    scanf(" %c", &lanjut);
    while (lanjut == 'y' || lanjut == 'Y') {
        printf("Pilih buku (1-%d): ", jumlahBuku);
        scanf("%d", &pilihanBuku[iBuku]);

        if (pilihanBuku[iBuku] < 1 || pilihanBuku[iBuku] > jumlahBuku) {
            printf("Pilihan tidak valid.\n");
            continue;
        }

        printf("Jumlah: ");
        scanf("%d", &jumlahBukuArr[iBuku]);

        total += daftarBuku[pilihanBuku[iBuku] - 1].harga * jumlahBukuArr[iBuku];

        printf("Tambah buku lain? (y/n): ");
        scanf(" %c", &lanjut);
        iBuku++;
    }

    printf("\n=== DAFTAR ALAT TULIS ===\n");
    for (int j = 0; j < jumlahAlatTulis; j++) {
        printf("%2d. %-25s - Rp%d\n", j + 1, daftarAlatTulis[j].nama, daftarAlatTulis[j].harga);
    }

    printf("\nBeli alat tulis? (y/n): ");
    scanf(" %c", &lanjut);
    while (lanjut == 'y' || lanjut == 'Y') {
        printf("Pilih alat tulis (1-%d): ", jumlahAlatTulis);
        scanf("%d", &pilihanAlatTulis[iAlat]);

        if (pilihanAlatTulis[iAlat] < 1 || pilihanAlatTulis[iAlat] > jumlahAlatTulis) {
            printf("Pilihan tidak valid.\n");
            continue;
        }

        printf("Jumlah: ");
        scanf("%d", &jumlahAlatTulisArr[iAlat]);

        total += daftarAlatTulis[pilihanAlatTulis[iAlat] - 1].harga * jumlahAlatTulisArr[iAlat];

        printf("Tambah alat tulis lain? (y/n): ");
        scanf(" %c", &lanjut);
        iAlat++;
    }

    // Hitung diskon
    if (total >= 300000) {
        diskon = 0.15;
    } else if (total >= 200000) {
        diskon = 0.10;
    } else if (total >= 100000) {
        diskon = 0.05;
    }

    // Diskon member
    if (member == 1) {
        diskon += 0.05; // tambahan 5%
    }

    float totalDiskon = total * diskon;
    float totalBayar = total - totalDiskon;

    // Untuk poin 1 poin = Rp10.000
    int poin = totalBayar / 10000;

    do {
        printf("\nTotal yang harus dibayar: Rp%.0f\n", totalBayar);
        printf("Masukkan uang pembayaran: Rp");
        scanf("%d", &bayar);

        if (bayar < totalBayar) {
            printf("Uang tidak cukup. Silakan masukkan kembali.\n");
        }
    } while (bayar < totalBayar);

    kembalian = bayar - totalBayar;

    // Struk
    printf("\n=====================================================\n");
    printf("                STRUK PEMBELIAN BUKU\n");
    printf("=====================================================\n");
    printf("Nama Pembeli : %s\n", namaPembeli);
    printf("Member       : %s\n", member ? "YA" : "TIDAK");

    if (iBuku > 0) {
        printf("\n-- Buku --\n");
        for (int j = 0; j < iBuku; j++) {
            printf("%-25s x %d = Rp%d\n",
                   daftarBuku[pilihanBuku[j] - 1].nama,
                   jumlahBukuArr[j],
                   daftarBuku[pilihanBuku[j] - 1].harga * jumlahBukuArr[j]);
        }
    }

    if (iAlat > 0) {
        printf("\n-- Alat Tulis --\n");
        for (int j = 0; j < iAlat; j++) {
            printf("%-25s x %d = Rp%d\n",
                   daftarAlatTulis[pilihanAlatTulis[j] - 1].nama,
                   jumlahAlatTulisArr[j],
                   daftarAlatTulis[pilihanAlatTulis[j] - 1].harga * jumlahAlatTulisArr[j]);
        }
    }

    printf("\nTotal Harga Awal : Rp%d\n", total);
    printf("Diskon (%.0f%%)     : Rp%.0f\n", diskon * 100, totalDiskon);
    printf("Total Bayar Akhir  : Rp%.0f\n", totalBayar);
    printf("Uang Dibayar       : Rp%d\n", bayar);
    printf("Kembalian          : Rp%d\n", kembalian);
    printf("Poin Diperoleh     : %d poin\n", poin);

    printf("\n=====================================================\n");
    printf("              Terima kasih sudah berbelanja!           \n");
    printf("=====================================================\n");

    return 0;
}
