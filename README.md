# PerhitunganKata
 Tugas 5 - Irfazi - 2210010277
 
# 1. Deskripsi Program
* Gunakan JTextArea dalam JScrollPane untuk input teks

* Setelah menekan tombol Hitung, hasil perhitungan berupa jumlah
kata dan karakter ditampilkan pada beberapa JLabel

# 2. Komponen GUI: 
JFrame, JPanel, JLabel, JTextArea, JScrollPane, JButton
- JPanel sebagai container utama.
- JTextArea untuk input teks dan letakkan dalam JScrollPane.
- JButton dengan label “Hitung Kata” untuk memicu perhitungan, "Cari" untuk memicu hasil pencarian kata, "Hapus" untuk menghapus input dan hasil, "Simpan File" digunakan untuk memicu penyimpanan, dan "Keluar" untuk keluar dari project.
- beberapa JLabel untuk menampilkan hasil jumlah kata, karakter, kalimat, paragraf, dan jumlah kemunculan kata.
- JTextField untuk input kata yang ingin dicari.

- JButton dengan label "Hapus"

private void btnHapusActionPerformed(java.awt.event.ActionEvent evt) {                                         
        btnHapus.addActionListener((ActionEvent e) -> {
        txtinput.setText("");  
        jmlKata.setText("0");
        jmlKarakter.setText("0");
        jmlKalimat.setText("0");
        jmlFaragraf.setText("0");
        jmlCari.setText("0");
        filedCari.setText(""); 
    });
    } 

Event ActionListener pada tombol ini untuk mengosongkan teks di JTextArea dan mengatur ulang label hasil perhitungan.
Dengan penambahan tombol "Hapus" ini, Anda dapat mengosongkan JTextArea dan mereset semua label perhitungan kembali ke nol secara langsung.

# 3. Logika Program: 
Manipulasi string, Ekspresi reguler


# 4. Events:
* ActionListener untuk tombol Hitung

private void btnHitungActionPerformed(java.awt.event.ActionEvent evt) {                                          
        btnHitung.addActionListener((ActionEvent e) -> {
        HitungKata(); 
    });
    }                                         

Penjelasan Kode :
hitungKata() berfungsi untuk menghitung jumlah kata, karakter, kalimat, dan paragraf dalam teks.
ActionListener pada tombol "Hitung" memicu fungsi hitungKata() ketika tombol ditekan.

- DocumentListener pada JTextArea memungkinkan perhitungan real-time saat teks diubah. 

private void HitungKata() {
        String text = txtinput.getText();

        int wordCount = text.isEmpty() ? 0 : text.split("\\s+").length;

        int charCount = text.length();

        int sentenceCount = text.isEmpty() ? 0 : text.split("[.!?]").length;

        int paragraphCount = text.isEmpty() ? 0 : text.split("\\n+").length;

        jmlKata.setText("" + wordCount);
        jmlKarakter.setText("" + charCount);
        jmlKalimat.setText("" + sentenceCount);
        jmlFaragraf.setText("" + paragraphCount);
        
    }

Penjelasan Kode :
Fungsi ini digunakan untuk menghitung jumlah kata, karakter, kalimat, dan paragraf:
- Jumlah Kata: Menggunakan split("\\s+") untuk hitung jumlah kata.
- Jumlah Karakter: Menggunakan text.length() untuk menghitung karakter total.
- Jumlah Kalimat: Menggunakan split("[.!?]") untuk memisahkan kalimat berdasarkan tanda baca. Perhitungan kalimat dilakukan dengan text.split("[.!?]"), yang membagi teks berdasarkan titik (.), tanda seru (!), atau tanda tanya (?). Setiap tanda ini dianggap sebagai akhir sebuah kalimat.
- Jumlah Paragraf: Menggunakan split("\\n+") untuk menghitung jumlah paragraf berdasarkan garis baru ganda sebagai pemisah. Perhitungan paragraf dilakukan dengan text.split("\\n+"), yang memisahkan teks setiap kali ada baris baru (\n). Setiap baris baru dianggap sebagai awal paragraf baru, dan jeda baris ganda (\n\n) dianggap sebagai pemisah antar paragraf.

* DocumentListener pada JTextArea untuk menghitung secara realtime

txtinput.getDocument().addDocumentListener(new DocumentListener() {
            public void changedUpdate(DocumentEvent e) { HitungKata(); }
            public void removeUpdate(DocumentEvent e) { HitungKata(); }
            public void insertUpdate(DocumentEvent e) { HitungKata(); }
        });
    }

Kode DocumentListener ini akan memanggil metode hitungText() setiap kali ada perubahan di textArea, baik saat teks ditambahkan atau dihapus, sehingga memungkinkan aplikasi untuk menghitung jumlah kata, karakter, kalimat, dan paragraf secara real-time.

# 5. Variasi:
* Tambahkan fitur untuk menghitung jumlah kalimat dan paragraf

 // Hitung jumlah kalimat menggunakan pemisah .!? untuk mengenali akhir kalimat
    int sentenceCount = text.isEmpty() ? 0 : text.split("[.!?]").length;

 // Hitung jumlah paragraf berdasarkan garis baru ganda sebagai pemisah
    int paragraphCount = text.isEmpty() ? 0 : text.split("\\n+").length;

// Update JLabel dengan hasil perhitungan
    jmlKalimat.setText("" + sentenceCount);
    jmlFaragraf.setText("" + paragraphCount);

* Implementasikan fungsi pencarian kata tertentu dalam teks

 private void btnCariActionPerformed(java.awt.event.ActionEvent evt) {                                        
        btnCari.addActionListener((ActionEvent e) -> {
            MencariKata();
        });
    } 

Penjelasan :
Metode MenjacriKata() menghitung jumlah kemunculan kata yang sesuai di dalam teks dan memperbarui jumlahkemunculankata.

  private void MencariKata() {
        String text = txtinput.getText();
        String searchWord = filedCari.getText();
        int count = 0;

        if (!searchWord.isEmpty()) {
            String[] words = text.split("\\s+");
            for (String word : words) {
                if (word.equalsIgnoreCase(searchWord)) {
                    count++;
                }
            }
        }
        
        jmlCari.setText(" " + count);
    }

  
* Sediakan opsi untuk menyimpan teks dan hasil perhitungan ke file

 private void btnSimpanActionPerformed(java.awt.event.ActionEvent evt) {                                          
        btnSimpan.addActionListener((ActionEvent e) -> {
            Simpan();
        });
    }    

Metode Simpan() membuat file hasil_penghitungan.txt dan menulis teks yang diinput beserta hasil perhitungan.
Jika penyimpanan berhasil, pesan konfirmasi akan ditampilkan.

private void Simpan() {
    JFileChooser fileChooser = new JFileChooser();
    fileChooser.setDialogTitle("Simpan Hasil Penghitungan");
    int userSelection = fileChooser.showSaveDialog(this);
    
    if (userSelection == JFileChooser.APPROVE_OPTION) {
        try (FileWriter writer = new FileWriter(fileChooser.getSelectedFile())) {
       
            writer.write("Teks:\n" + txtinput.getText() + "\n\n");
            writer.write("Jumlah Kata: " + jmlKata.getText() + "\n");
            writer.write("Jumlah Karakter: " + jmlKarakter.getText() + "\n");
            writer.write("Jumlah Kalimat: " + jmlKalimat.getText() + "\n");
            writer.write("Jumlah Paragraf: " + jmlFaragraf.getText() + "\n");
            writer.write("Pencarian Kata '" + filedCari.getText() + "': " + jmlCari.getText() + "\n");
            JOptionPane.showMessageDialog(this, "Hasil berhasil disimpan ke hasil_penghitungan.txt");
        } catch (IOException e) {
            JOptionPane.showMessageDialog(this, "Gagal menyimpan file: " + e.getMessage());
        }
        }
    }

Dengan kode ini, sebuah dialog JFileChooser akan muncul sehingga Anda bisa memilih atau menentukan lokasi penyimpanan file hasil penghitungan sesuai keinginan.


## Contoh Gambar Project Setelah di Run
![](https://github.com/Irfazi/PerhitunganKata/blob/main/Screenshot%202024-11-17%20194317.png)

## Indikator Penilaian:

| No  | Komponen         |  Persentase  |
| :-: | --------------   |   :-----:    |
|  1  | Komponen GUI     |    10    |
|  2  | Logika Program   |    20    |
|  3  |  Events          |    10    |
|  4  | Kesesuaian UI    |    20    |
|  5  | Memenuhi Variasi |    40    |
|     | TOTAL        | 100 |

