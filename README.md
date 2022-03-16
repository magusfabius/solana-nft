# buildspace Solana NFT Drop Project with Fabius notes
### Welcome 👋
To get started with this course, clone this repo and follow these commands:

1. cd into the `app` folder
2. Run `npm install` at the root of your directory
3. Run `npm run start` to start the project
4. Start coding!

### What is the .vscode Folder?
If you use VSCode to build your app, we included a list of suggested extensions that will help you build this project! Once you open this project in VSCode, you will see a popup asking if you want to download the recommended extensions :).

### Questions?
Have some questions make sure you head over to your [buildspace Dashboard](https://app.buildspace.so/projects/CO77556be5-25e9-49dd-a799-91a2fc29520e) and link your Discord account so you can get access to helpful channels and your instructor!


# Notes

Creating NFT with Solana:

pros:
- is cheaper, less fee
- is faster than Ethereum because there are built in smart contracts and functions that manage every exceptions
    - and here could happen more errors because Solana permits parallel transactions
    - code is less complex

cons:
- getting Solana running and working is not easy right now (March 2022)
    - Solana is a really early piece of technology and because it's so early it's changing often so it's hard to just Google a question or get a clear, concise answer
    - don't expect a super clean developer experience. You will likely run into random bumps and it's up to you to figure out an answer + help others
    - today, 9 March 2022, I'm not able to upload NFTs, after some searches it looks like there is a complication with the network itself
        - 14 March 2022 - finally uploaded the NFT, everything's running now
- Only PNGs are supported right now via the CLI. For other file types like MP4, MP3, HTML, etc you need to create a custom script

### Tools

1. Metaplex CLI
With Metaplex we don't need to write our own contract. 
Metaplex has already deployed its own standard NFT contracts that any dev can interact with and build their own NFT collections on.
This is kinda wild. It's like a smart-contract-as-a-service lol.
Installation: git clone -b v1.1.1 https://github.com/metaplex-foundation/metaplex.git
              yarn install --cwd ~/metaplex/js/

2. Solana CLI
The Solana CLI will allow us to deploy to devnet, an actual blockchain run by real validators.
Installation: sh -c "$(curl -sSfL https://release.solana.com/stable/install)"


### Useful Solana CLI commands 
- solana config get
- solana address
- solana balance
- solana airdrop <AMOUNT>



### Errors Troubleshooting
- EACESS when installing packages
    - always use sudo
    - reinstall npm: npm install -g npm

- when "solana airdrop 2" -> "Error: airdrop request failed. This can happen when the rate limit is reached."
    - solana airdrop <AMOUNT> <RECIPIENT_ACCOUNT_ADDRESS> --url https://api.devnet.solana.com
    - and then if you wanna get the balance: solana balance <ACCOUNT_ADDRESS> --url https://api.devnet.solana.com

- Error: Transaction was not confirmed in 60.01 seconds. (9 March 2022)
    - Just wanted to give an update regarding Candy Machine on Devnet. As you may know, there has been some complications with the Candy Machine program on Devnet for the past few days which has resulted in many Transaction was not confirmed in 60.01 seconds errors. This is a complication with the network itself. 


### STEPS

- generate local wallet: solana-keygen new --outfile ~/.config/solana/devnet.json
    - set it as default: solana config set --keypair ~/.config/solana/devnet.json
    - put some solana in it with solana airdrop

- set candymachine configuration ./config.json

- upload NFTs
    - ts-node ~/metaplex/js/packages/cli/src/candy-machine-v2-cli.ts upload -e devnet -k ~/.config/solana/devnet.json -cp config.json ./assets

- verify upload 
    - check if the .cache folder was created
    - ts-node ~/metaplex/js/packages/cli/src/candy-machine-v2-cli.ts verify_upload -e devnet -k ~/.config/solana/devnet.json   

    - Note: if you get an error like "no such file or directory, scandir './assets'" it means you ran the command from the wrong place. Be sure to run it in the same directory where your assets folder is.

- update candymachine
    - if you change the configuration of the candymachine you need to update it
    - ts-node ~/metaplex/js/packages/cli/src/candy-machine-v2-cli.ts update_candy_machine -e devnet  -k ~/.config/solana/devnet.json -cp config.json


### Deploy using Vercel

1. upload the project on github
2. ignore .cache and .env by adding them in .gitignore
3. go on Vercel and select the github project
4. add ENVIROMENT VARIABLES that were in .env plus add the variable with name CI and value 'False' to skip the warning problems while building 

# preview
link https://solana-nft-six.vercel.app/






