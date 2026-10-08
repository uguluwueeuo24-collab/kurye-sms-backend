const express = require('express');
const cors = require('cors');

const app = express();
app.use(cors());
app.use(express.json());

// Sadece SMS İşlerini Yürüten Sunucu Endpoint'i
app.post('/api/send-sms', (req, res) => {
  const { courierPhone, customerName, customerPhone, address, items, bagCount, extraFee, notes } = req.body;

  // SMS İletim Formatı
  const smsText = `BESEVLER JET KURYE SIPARISI\n` +
    `Musteri: ${customerName}\n` +
    `Tel: ${customerPhone}\n` +
    `Adres: ${address}\n` +
    `Alinacaklar: ${items}\n` +
    `Poset: ${bagCount || 0} Adet\n` +
    `Kurye Ek Ucret: ${extraFee} TL\n` +
    `Not: ${notes || 'Yok'}`;

  // Kullanıcının SMS uygulamasını açıp kuryeye SMS göndermesini sağlayan yönlendirme adresi
  const targetNumber = courierPhone || "05xxxxxxxxx"; // Varsayılan numara
  const smsUrl = `sms:${targetNumber}?body=${encodeURIComponent(smsText)}`;

  console.log(`[SMS SUNUCUSU] ${customerName} isimli müşterinin siparişi ${targetNumber} numarasına yönlendirildi.`);

  res.json({
    success: true,
    message: "SMS sunucusu siparişi başarıyla işledi.",
    smsUrl: smsUrl
  });
});

const PORT = process.env.PORT || 10000;
app.listen(PORT, () => console.log(`SMS Sunucusu ${PORT} portunda başarıyla çalışıyor.`));
