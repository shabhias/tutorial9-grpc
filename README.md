# REFLECTION

1. What are the key differences between unary, server streaming, and bi-directional streaming RPC (Remote Procedure Call) methods, and in what scenarios would each be most suitable?

- RPC Unary merupakan jenis RPC paling sederhana di mana klien mengirim satu permintaan ke server dan menerima satu respons sebagai balasan. Jenis RPC ini Digunakan dalam situasi permintaan dan respons sederhana seperti autentikasi atau pengiriman formulir.


- RPC Streaming Server dimana klien emngirim satu permintaan  ke server dan menerima respons dalam bentuk stream yang terdiri dari beberapa pesan. Jenis RPC ini Cocok digunakan ketika server perlu mengirimkan sejumlah besar data, misalnya daftar besar atau file, kepada klien.

- RPC Bi-directional Streaming di mana Klien dan server dapat mengirim serangkaian pesan menggunakan stream yang dapat dibaca dan ditulis (read-write). RPC ini Ideal untuk aplikasi yang memerlukan pertukaran data besar antara klien dan server secara independen, seperti aplikasi obrolan.


2. What are the potential security considerations involved in implementing a gRPC service in Rust, particularly regarding authentication, authorization, and data encryption?

- Autentikasi diperlukan untuk memastikan keamanan. Mekanisme autentikasi seperti sertifikat klien SSL/TLS atau sistem token perlu diintegrasikan dan divalidasi.
-  Otorisasi diperlukan logika otorisasi yang efektif untuk menegakkan kebijakan kontrol akses. Otorsisasi perlu diterapkan pada setiap akses data dalam gRPC. 
- Enkripsi data diperlukan untuk menjaga privasi data. Penggunaan SSL/TLS untuk melindungi saluran komunikasi dan mencegah akses tidak sah.


3. What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC, especially in scenarios like chat applications?

Streaming dua arah dalam gRPC Rust menghadapi tantangan dalam manajemen konkurensi, penanganan kesalahan, dan penataan pesan. Memastikan komunikasi yang lancar antara klien dan server, menangani kesalahan dengan efektif, dan mengelola aliran pesan yang benar-benar penting. Tantangan lainnya termasuk penanganan tekanan balik, alokasi sumber daya, dan memastikan keamanan serta skalabilitas. Mengatasi tantangan-tantangan ini penting untuk menjaga kinerja dan kehandalan, terutama dalam aplikasi obrolan di mana interaksi real-time sangat diperlukan.


4. What are the advantages and disadvantages of using the tokio_stream::wrappers::ReceiverStream for streaming responses in Rust gRPC services?

- Keunggulannya adalah Integrasi yang mulus dengan runtime asinkron Tokio, cocok untuk aplikasi yang sudah menggunakan Tokio untuk I/O asinkron, Fleksibilitas dalam menangani berbagai jenis stream, dan Memungkinkan streaming asinkron data, sehingga layanan Rust gRPC dapat menangani respons streaming tanpa memblokir event loop.

- Kerugiannya adalah bahwa ReceiverStream tidak menyediakan dukungan built-in untuk mengelola kesalahan atau buffering data secara otomatis, sehingga kita perlu menangani ini secara manual. Ini bisa menjadi kompleksitas tambahan terutama dalam skenario di mana penanganan kesalahan dan manajemen aliran data yang baik sangat penting, seperti dalam streaming gRPC.


5. In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity, promoting maintainability and extensibility over time?

Untuk meningkatkan penggunaan ulang dan modularitas, serta mempromosikan kemudahan pemeliharaan dan perluasan kode dari waktu ke waktu, kode gRPC Rust dapat diorganisir dengan memisahkan layanan ke dalam modul terpisah berdasarkan fungsionalitas terkait, dan memisahkan definisi pesan ke dalam file terpisah. Dengan pendekatan ini, setiap layanan menjadi mandiri dan mudah diuji, sementara definisi pesan dapat digunakan kembali di berbagai layanan, memungkinkan pengembangan yang lebih efisien dan fleksibel.


6. In the MyPaymentService implementation, what additional steps might be necessary to handle more complex payment processing logic?

Peningkatan Implementasi MyPaymentServive untuk menangani logika permrosesan pembayaran yang lebih kompleks, perlu dilakukan perubahan pada implementasi MyPaymentService. Metode process_payment dapat diubah menjadi server streaming untuk mengirimkan respons secara bertahap kepada klien.Ini memungkinkan pengiriman data yang lebih kompleks dengan lebih efisien, karena respons dapat dikirimkan secara bertahap selama proses pemrosesan pembayaran.


7. What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of distributed systems, particularly in terms of interoperability with other technologies and platforms?

Adopsi gRPC berdampak pada arsitektur dan desain sistem terdistribusi dengan menyediakan komunikasi yang efisien, kontrak layanan yang tidak bergantung pada bahasa pemrograman, dan kemampuan streaming dua arah. Ini meningkatkan interoperabilitas dengan fitur seperti transcoding JSON dan dukungan HTTP/1.x, sementara juga mempromosikan sistem yang skalabel, fault-tolerant, dan kompatibel dengan arsitektur mikroservis modern serta dapat berintegrasi dengan infrastruktur legacy.


8. What are the advantages and disadvantages of using HTTP/2, the underlying protocol for gRPC, compared to HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs?

- Keunggulan Penggunaan HTTP/2 untuk gRPC adalah Multiplexing, kompresi header, server push, dan prioritas stream berpengaruh kepada Penurunan latency, peningkatan efisiensi, dan penggunaan sumber daya jaringan yang lebih baik.

- Tangangan penggunaan  HTTP/2 adalah Kompleksitas yang meningkat dalam implementasi dan debugging dibandingkan dengan HTTP/1.1.

- Meskipun HTTP/2 mendukung komunikasi dua arah, WebSocket lebih cocok untuk skenario komunikasi real-time dan full-duplex.

- Faktor penentu antara HTTP/2, HTTP/1.1, atau WebSocket tergantung pada persyaratan kinerja, kendala kompatibilitas, dan kasus penggunaan API yang spesifik.


9. How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in terms of real-time communication and responsiveness?

Model request-response dari API REST berbeda dengan kemampuan streaming dua arah dari gRPC dalam hal komunikasi real-time dan responsif. API REST menggunakan model request-response, sedangkan gRPC menyediakan streaming dua arah untuk komunikasi real-time. API REST lebih cocok untuk interaksi stateless, sementara gRPC lebih unggul dalam skenario yang memerlukan pembaruan terus-menerus, seperti aplikasi obrolan. Dengan menggunakan streaming dua arah, gRPC memungkinkan pertukaran data instan yang lebih responsif daripada API REST.


10. What are the implications of the schema-based approach of gRPC, using Protocol Buffers, compared to the more flexible, schema-less nature of JSON in REST API payloads?

- gRPC dengan Protocol Buffer menawarkan kompatibilitas yang baik, kinerja yang lebih tinggi, dan alat yang lebih baik karena menggunakan pendekatan berbasis skema. Cocok untuk skenario yang membutuhkan strong typing dan kinerja yang kuat.

- JSON dalam REST API Memberikan fleksibilitas dan keterbacaan di berbagai bahasa dan platform. Namun bisa mengakibatkan biaya tambahan dalam beberapa kasus.

- gRPC lebih diuntungkan untuk skenario yang memprioritaskan strong typing dan kinerja yang kuat, sementara JSON dalam REST API sesuai untuk situasi yang mengutamakan fleksibilitas dan keterbacaan.