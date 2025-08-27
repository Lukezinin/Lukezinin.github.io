<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8">
  <title>Chat Simples</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      display: flex;
      flex-direction: column;
      height: 100vh;
      margin: 0;
      background: #f4f4f4;
    }
    header {
      background: #4CAF50;
      color: white;
      text-align: center;
      padding: 10px;
    }
    #chat {
      flex: 1;
      padding: 10px;
      overflow-y: auto;
      background: white;
      border: 1px solid #ccc;
      margin: 10px;
    }
    #form {
      display: flex;
      padding: 10px;
      background: #ddd;
    }
    #msg {
      flex: 1;
      padding: 8px;
      font-size: 14px;
    }
    button {
      padding: 8px 15px;
      background: #4CAF50;
      color: white;
      border: none;
      cursor: pointer;
    }
    button:hover {
      background: #45a049;
    }
  </style>
</head>
<body>
  <header><h2>💬 Chat Simples</h2></header>
  
  <div
