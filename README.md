<!DOCTYPE html><html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Web3 Developer Portfolio</title>
    <script src="https://cdn.jsdelivr.net/npm/web3@latest/dist/web3.min.js"></script>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; background-color: #0d1117; color: white; }
        .container { max-width: 800px; margin: auto; padding: 20px; }
        .card { background: #161b22; padding: 20px; margin: 20px 0; border-radius: 10px; }
        a { color: #58a6ff; text-decoration: none; }
        button { background: #58a6ff; color: white; border: none; padding: 10px 20px; cursor: pointer; border-radius: 5px; margin-top: 10px; }
    </style>
</head>
<body>
    <div class="container">
        <h1>👨‍💻 Web3 Developer Portfolio</h1>
        <p>Hello, I am <strong>Your Name</strong>, a passionate Web3 & Blockchain Developer.</p><div class="card">
        <h2>About Me</h2>
        <p>Experienced in Solidity, Web3.js, and building decentralized applications (DApps).</p>
    </div>

    <div class="card">
        <h2>Projects</h2>
        <ul>
            <li><a href="#">NFT Marketplace - Buy & Sell NFTs</a></li>
            <li><a href="#">DeFi Staking Platform</a></li>
            <li><a href="#">Ethereum Smart Contracts</a></li>
        </ul>
    </div>

    <div class="card">
        <h2>Connect Wallet</h2>
        <button onclick="connectWallet()">Connect MetaMask</button>
        <p id="wallet-address"></p>
    </div>

    <div class="card">
        <h2>Mint NFT</h2>
        <button onclick="mintNFT()">Mint NFT</button>
        <p id="nft-status"></p>
    </div>

    <div class="card">
        <h2>Token Balance</h2>
        <button onclick="checkBalance()">Check Balance</button>
        <p id="token-balance"></p>
    </div>

    <div class="card">
        <h2>Contact</h2>
        <p>Email: yourname@email.com</p>
        <p>GitHub: <a href="https://github.com/yourgithub">github.com/yourgithub</a></p>
    </div>
</div>

<script>
    let web3;
    let account;
    const nftContractAddress = "0xYourNFTContractAddress";
    const tokenContractAddress = "0xYourTokenContractAddress";

    async function connectWallet() {
        if (window.ethereum) {
            try {
                web3 = new Web3(window.ethereum);
                const accounts = await ethereum.request({ method: 'eth_requestAccounts' });
                account = accounts[0];
                document.getElementById("wallet-address").innerText = "Connected: " + account;
            } catch (error) {
                console.error("User denied account access");
            }
        } else {
            alert("MetaMask not detected. Please install MetaMask.");
        }
    }

    async function mintNFT() {
        if (!account) return alert("Connect wallet first!");
        document.getElementById("nft-status").innerText = "Minting NFT...";
        try {
            const contract = new web3.eth.Contract([], nftContractAddress);
            await contract.methods.mint().send({ from: account });
            document.getElementById("nft-status").innerText = "NFT Minted Successfully!";
        } catch (error) {
            console.error(error);
            document.getElementById("nft-status").innerText = "Minting Failed";
        }
    }

    async function checkBalance() {
        if (!account) return alert("Connect wallet first!");
        try {
            const contract = new web3.eth.Contract([], tokenContractAddress);
            const balance = await contract.methods.balanceOf(account).call();
            document.getElementById("token-balance").innerText = `Token Balance: ${balance}`;
        } catch (error) {
            console.error(error);
            document.getElementById("token-balance").innerText = "Error fetching balance";
        }
    }
</script>

</body>
</html>
