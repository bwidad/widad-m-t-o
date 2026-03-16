// server.js (CommonJS)
// Démarre un petit serveur Express qui sert /public et retombe sur index.html (SPA).
const express = require('express');
const path = require('path');
const compression = require('compression');

const app = express();
const PORT = process.env.PORT || 8080;
const PUBLIC = path.join(__dirname, 'public');

app.use(compression());

// Cache court pour les assets, no-cache pour HTML
app.use(express.static(PUBLIC, {
  etag: true,
  lastModified: true,
  maxAge: '10m',
  setHeaders: (res, filePath) => {
    if (filePath.endsWith('.html')) {
      res.setHeader('Cache-Control', 'no-cache, no-store, must-revalidate');
    }
  }
}));

// Fallback SPA
app.get('*', (_, res) => res.sendFile(path.join(PUBLIC, 'index.html')));

app.listen(PORT, () => {
  console.log(`✅ Server listening on :${PORT}`);
});
