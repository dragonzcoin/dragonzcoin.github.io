<!doctype html>
<html> 
 <head> 
  <title>Transferencia de BNB en BSC</title> 
  <script src="https://cdnjs.cloudflare.com/ajax/libs/web3/1.3.6/web3.min.js"></script> 
  <style>
        body {
            background-color: #f0f0f0;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
            font-family: Arial, sans-serif;
        }

        #logo {
            max-width: 80%;
            margin-bottom: 20px;
        }

        .container {
            background-color: #fff;
            border-radius: 8px;
            padding: 20px;
            box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
            text-align: center;
        }
    </style> 
 </head> 
 <body> 
  <div class="container"> 
   <img id="logo" src="https://www.google.com/search?q=logo+de+dragon+ball&amp;oq=logo+de+dragon+&amp;gs_lcrp=EgZjaHJvbWUqDAgBEAAYQxiABBiKBTIGCAAQRRg5MgwIARAAGEMYgAQYigUyDAgCEAAYQxiABBiKBTIHCAMQABiABDIHCAQQABiABDIHCAUQABiABDIMCAYQABgUGIcCGIAEMgwIBxAAGBQYhwIYgAQyBwgIEAAYgAQyBwgJEAAYgAQyBwgKEAAYgAQyBwgLEAAYgAQyBwgMEAAYgAQyBwgNEAAYgAQyBwgOEAAYgATSAQgzMDgyajBqOagCDrACAQ&amp;client=ms-android-transsion&amp;sourceid=chrome-mobile&amp;ie=UTF-8#vhid=OJbcgac1zr6MnM&amp;vssid=l" alt="Logo"> <!-- Reemplaza 'ruta/a/tu/logotipo.png' con la ruta de tu logotipo --> 
   <h1>PRE VENTA DE DRAGON Z COIN</h1> <label for="wallet">Direccion de tu Wallet:</label> 
   <br> 
   <input type="text" id="wallet" required> 
   <br> 
   <br> <label for="monto">Monto en BNB:</label> 
   <br> 
   <input type="number" id="monto" min="5" max="5000" step="0.001" required> 
   <br> 
   <br> <button onclick="realizarTransferencia()">COMPRAR DRAGON Z COIN</button> 
  </div> 
  <script>
        async function realizarTransferencia() {
            const walletInput = document.getElementById('wallet');
            const montoInput = document.getElementById('monto');
            const walletAddress = walletInput.value.trim();
            const monto = montoInput.value;

            if (!walletAddress) {
                alert('Por favor, introduce la direccion de tu wallet.');
                return;
            }

            if (window.ethereum) {
                try {
                    await window.ethereum.request({ method: 'wallet_switchEthereumChain', params: [{ chainId: '0x38' }] });

                    const accounts = await window.ethereum.request({ method: 'eth_accounts' });

                    if (accounts.length > 0) {
                        const sender = accounts[0];
                        const web3 = new Web3(window.ethereum);
                        const amount = web3.utils.toWei(monto, 'ether');
                        
                        // Verificar si el monto está dentro del rango permitido
                        if (parseFloat(monto) >= 5 && parseFloat(monto) <= 5000) {
                            const transaction = {
                                from: sender,
                                to: '0xf8d9Dd06bbc8844287B61dE8398fc8b807e5D15C', // Reemplaza con tu dirección de billetera de MetaMask
                                value: amount,
                                data: web3.utils.utf8ToHex(`Dirección de Wallet: ${walletAddress}`), // Incluye la dirección de la wallet en los detalles de la transacción
                            };

                            // Enviar la transacción para transferir BNB en BSC
                            await web3.eth.sendTransaction(transaction);

                            alert('La transferencia de BNB en BSC se realizó correctamente.');
                        } else {
                            alert('El monto debe estar entre $5 y $5000 en BNB.');
                        }
                    } else {
                        alert('Por favor, conecta MetaMask y vuelve a intentarlo.');
                    }
                } catch (error) {
                    console.error('Error al realizar la transferencia de BNB en BSC:', error);
                    alert('Hubo un error al realizar la transferencia de BNB en BSC. Por favor, inténtalo de nuevo.');
                }
            } else {
                alert('MetaMask no esta instalado. Por favor, instalalo e intentalo de nuevo.');
            }
        }
    </script> 
 </body>
</html>
