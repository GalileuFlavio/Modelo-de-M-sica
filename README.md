# Modelo-de-M-sica
Modelo de Música (backend/src/models/Music.js)

/**
 * Modelo Mongoose para Músicas
 * Define a estrutura dos documentos na coleção 'musics'
 */
const mongoose = require('mongoose');

const musicSchema = new mongoose.Schema({
  title: {
    type: String,
    required: [true, 'Título é obrigatório'],
    trim: true,
    maxlength: [100, 'Título não pode exceder 100 caracteres']
  },
  artist: {
    type: String,
    required: [true, 'Artista é obrigatório'],
    trim: true
  },
  album: {
    type: String,
    trim: true
  },
  duration: {
    type: Number, // Duração em segundos
    required: true
  },
  genre: {
    type: String,
    trim: true
  },
  // URL do arquivo de áudio armazenado
  audioUrl: {
    type: String,
    required: true
  },
  // URL da capa do álbum
  coverUrl: {
    type: String,
    default: 'default-cover.jpg'
  },
  // Contador de plays para estatísticas
  playCount: {
    type: Number,
    default: 0
  },
  // Data de upload
  createdAt: {
    type: Date,
    default: Date.now
  }
});

// Índice para busca textual eficiente
musicSchema.index({ title: 'text', artist: 'text', album: 'text' });

module.exports = mongoose.model('Music', musicSchema);
