```kotlin
/**
 * Implementasi Enkapsulasi Kotlin
 * Tema 14: E-Course ITK (Pendaftaran Pelatihan)
 */

// Entitas: Peserta 
class Peserta(val id: String, val nama: String)

// Entitas: Instruktur 
class Instruktur(val nama: String, val spesialisasi: String)

// Entitas Utama: KelasKursus 
class KelasKursus(
    val namaKursus: String, 
    val instruktur: Instruktur, 
    private val batasMaksimal: Int // Data Hiding: Akses dibatasi 
) {

    // Enkapsulasi Mutlak: Daftar siswa tidak boleh diakses langsung dari luar 
    private val _daftarSiswaAktif = mutableListOf<Peserta>()

    // Jalur Resmi untuk mendaftar dengan validasi Aturan Bisnis 
    fun daftarPelatihan(peserta: Peserta) {
        println("--- Mencoba Pendaftaran: ${peserta.nama} ---")
        
        // Aturan Bisnis: Pendaftaran ditolak jika kelas penuh 
        if (_daftarSiswaAktif.size < batasMaksimal) {
            _daftarSiswaAktif.add(peserta) // Masuk ke "Daftar Siswa Aktif" [cite: 106]
            println("Status: SUKSES. ${peserta.nama} berhasil terdaftar.")
        } else {
            // Simulasi GAGAL: Memunculkan print error 
            println("Status: GAGAL. Kelas $namaKursus telah mencapai batas maksimal ($batasMaksimal).")
        }
        println("------------------------------------------")
    }

    fun tampilkanSiswa() {
        println("Daftar Siswa Aktif ($namaKursus):")
        _daftarSiswaAktif.forEach { println("- ${it.nama}") }
    }
}

fun main() {
    // Inisialisasi Objek
    val dosen = Instruktur("Bapak Himawan", "PBO")
    // Simulasi dengan batas maksimal 2 orang 
    val kelasPBO = KelasKursus("Pemrograman Kotlin", dosen, 2)

    val mhs1 = Peserta("001", "Irfan")
    val mhs2 = Peserta("002", "Rival")
    val mhs3 = Peserta("003", "Rubian")

    // --- SIMULASI SUKSES --- 
    kelasPBO.daftarPelatihan(mhs1)
    kelasPBO.daftarPelatihan(mhs2)

    // --- SIMULASI GAGAL (Aturan Bisnis Terlampaui) 
    kelasPBO.daftarPelatihan(mhs3)

    // Menampilkan hasil akhir 
    kelasPBO.tampilkanSiswa()
}
```
