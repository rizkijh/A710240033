class Rekening:
    def __init__(self, nomor_rekening, nama_pemilik, saldo_awal, jenis_rekening, nama_bank):
        """
        Konstruktor untuk kelas Rekening.

        Args:
            nomor_rekening (str): Nomor unik rekening.
            nama_pemilik (str): Nama pemilik rekening.
            saldo_awal (float): Saldo awal saat rekening dibuka.
            jenis_rekening (str): Jenis rekening (misalnya, Tabungan, Giro).
            nama_bank (str): Nama bank tempat rekening dibuka.
        """
        self.nomor_rekening = nomor_rekening
        self.nama_pemilik = nama_pemilik
        self.saldo = saldo_awal
        self.jenis_rekening = jenis_rekening
        self.nama_bank = nama_bank
        print(f"Rekening {self.nomor_rekening} atas nama {self.nama_pemilik} berhasil dibuat di {self.nama_bank}.")

    def setor(self, jumlah):
        """
        Metode untuk melakukan setoran ke rekening.

        Args:
            jumlah (float): Jumlah uang yang akan disetor.

        Returns:
            str: Pesan status setoran.
        """
        if jumlah > 0:
            self.saldo += jumlah
            return f"Setoran Rp{jumlah:,.2f} berhasil. Saldo baru: Rp{self.saldo:,.2f}"
        else:
            return "Jumlah setoran tidak valid."

    def tarik(self, jumlah):
        """
        Metode untuk melakukan penarikan dari rekening.

        Args:
            jumlah (float): Jumlah uang yang akan ditarik.

        Returns:
            str: Pesan status penarikan.
        """
        if jumlah > 0:
            if self.saldo >= jumlah:
                self.saldo -= jumlah
                return f"Penarikan Rp{jumlah:,.2f} berhasil. Saldo baru: Rp{self.saldo:,.2f}"
            else:
                return "Saldo tidak mencukupi untuk penarikan."
        else:
            return "Jumlah penarikan tidak valid."

    def cek_saldo(self):
        """
        Metode untuk mengecek saldo saat ini.

        Returns:
            str: Informasi saldo saat ini.
        """
        return f"Saldo rekening {self.nomor_rekening} atas nama {self.nama_pemilik}: Rp{self.saldo:,.2f}"

    def transfer(self, rekening_tujuan, jumlah):
        """
        Metode untuk mentransfer dana ke rekening lain.

        Args:
            rekening_tujuan (Rekening): Objek rekening tujuan.
            jumlah (float): Jumlah uang yang akan ditransfer.

        Returns:
            str: Pesan status transfer.
        """
        if jumlah > 0:
            if self.saldo >= jumlah:
                self.saldo -= jumlah
                rekening_tujuan.terima_transfer(jumlah, self.nama_pemilik) # Memanggil metode di rekening tujuan
                return f"Transfer Rp{jumlah:,.2f} ke rekening {rekening_tujuan.nomor_rekening} ({rekening_tujuan.nama_pemilik}) berhasil. Saldo baru: Rp{self.saldo:,.2f}"
            else:
                return "Saldo tidak mencukupi untuk transfer."
        else:
            return "Jumlah transfer tidak valid."

    def terima_transfer(self, jumlah, nama_pengirim):
        """
        Metode internal untuk menerima dana transfer.

        Args:
            jumlah (float): Jumlah uang yang diterima.
            nama_pengirim (str): Nama pengirim dana.
        """
        self.saldo += jumlah
        print(f"Rekening {self.nomor_rekening} ({self.nama_pemilik}) menerima transfer Rp{jumlah:,.2f} dari {nama_pengirim}.")


    def info_rekening(self):
        """
        Metode untuk menampilkan informasi lengkap rekening.

        Returns:
            str: Informasi detail rekening.
        """
        return (f"\n--- Informasi Rekening ---"
                f"\nBank             : {self.nama_bank}"
                f"\nNomor Rekening   : {self.nomor_rekening}"
                f"\nNama Pemilik     : {self.nama_pemilik}"
                f"\nJenis Rekening   : {self.jenis_rekening}"
                f"\nSaldo            : Rp{self.saldo:,.2f}")
