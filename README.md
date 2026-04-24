// E-Course ITK (Pendaftaran Pelatihan)

class Peserta(val id: String, val nama: String)

class Instruktur(val nama: String, val spesialisasi: String)

class KelasKursus(
    val namaKursus: String, 
    val instruktur: Instruktur, 
    private val batasMaksimal: Int // Enkapsulasi: Batas tidak bisa diubah dari luar
) {

    // Enkapsulasi Mutlak: Koleksi siswa tidak boleh diakses langsung 
    private val _daftarSiswaAktif = mutableListOf<Peserta>()

    // Fungsi untuk mendaftarkan peserta dengan validasi Aturan Bisnis
    fun daftarPelatihan(peserta: Peserta) {
        println("=== Mencoba Pendaftaran: ${peserta.nama} ===")
        
        // Aturan Bisnis: Pendaftaran ditolak jika kelas mencapai batas maksimal 
        if (_daftarSiswaAktif.size < batasMaksimal) {
            _daftarSiswaAktif.add(peserta) // Berhasil ditambahkan ke "Daftar Siswa Aktif" 
            println("Status: BERHASIL. Selamat bergabung di kelas $namaKursus.")
            println("Slot Terisi: ${_daftarSiswaAktif.size} / $batasMaksimal")
        } else {
            // Simulasi GAGAL: Menolak karena kuota penuh
            println("Status: GAGAL. Mohon maaf, kuota kelas $namaKursus sudah penuh.")
        }
        println("-------------------------------------------")
    }

    fun tampilkanLaporan() {
        println("\nLAPORAN KELAS: $namaKursus")
        println("Instruktur: ${instruktur.nama}")
        println("Total Peserta Aktif: ${_daftarSiswaAktif.size}")
        _daftarSiswaAktif.forEach { println("- ${it.nama} (ID: ${it.id})") }
    }
}

fun main() {
    // Inisialisasi Objek
    val dosen = Instruktur("Bapak Himawan", "Object Oriented Programming")
    // Simulasi dengan batas maksimal 2 peserta
    val kelasPBO = KelasKursus("PBO Kotlin", dosen, 2)

    val mhs1 = Peserta("04221001", "Fajar")
    val mhs2 = Peserta("04221029", "Irfan")
    val mhs3 = Peserta("04221044", "Rubian")

    // 1. Simulasi SUKSES (Aksi yang sah)
    kelasPBO.daftarPelatihan(mhs1)
    kelasPBO.daftarPelatihan(mhs2)

    // 2. Simulasi GAGAL (Melanggar aturan bisnis: Kuota Habis)
    // Pendaftaran mhs3 akan memicu pesan error karena batas maksimal adalah 2
    kelasPBO.daftarPelatihan(mhs3)

    // Tampilkan hasil akhir pendaftaran
    kelasPBO.tampilkanLaporan()
}
