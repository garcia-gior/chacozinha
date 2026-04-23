# 🏡 Chá de Casa Nova — Esther Donesi

## 📁 Arquivos para subir no GitHub
index.html + esther.jpg

## 🚀 Deploy
1. Crie repo no GitHub (ex: cha-esther)
2. Suba index.html + esther.jpg
3. Importe no Vercel → deploy automático

## 📊 Planilha
https://docs.google.com/spreadsheets/d/1FgmSZVKYL6FlU0nPj8kf87nCqOHEaYU4/edit

## Apps Script (Extensões → Apps Script na planilha)
Cole o código abaixo e publique como Web App (qualquer pessoa):

```
const SS = SpreadsheetApp.getActiveSpreadsheet();
function doGet(e) {
  if (e.parameter.action === 'getTaken') {
    const sheet = SS.getSheetByName('🔒 Itens Reservados');
    const data = sheet.getDataRange().getValues();
    const takenIds = data.slice(2).map(r => Number(r[0])).filter(n => !isNaN(n) && n > 0);
    return ContentService.createTextOutput(JSON.stringify({ takenIds })).setMimeType(ContentService.MimeType.JSON);
  }
  return ContentService.createTextOutput('ok');
}
function doPost(e) {
  const body = JSON.parse(e.postData.contents);
  SS.getSheetByName('📋 Respostas').appendRow([new Date(), body.name, body.phone, body.email||'', body.items.join(', '), body.itemIds.join(', '), '✅ Confirmado']);
  body.itemIds.forEach(id => SS.getSheetByName('🔒 Itens Reservados').appendRow([id, '', body.name]));
  return ContentService.createTextOutput('ok');
}
```

Após publicar, substitua no index.html:
const SHEETS_URL = 'SUA_URL_DO_APPS_SCRIPT_AQUI';

## 📍 Evento
07/06/2026 às 15h · Av. dos Guatambus, 53 – Eldorado, SP · CEP 04476-420
