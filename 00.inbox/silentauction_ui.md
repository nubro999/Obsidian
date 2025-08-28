Architecture

  - Framework: Next.js 14 with React 18
  - Blockchain: Integrated with Mina Protocol using o1js
  - Styling: Tailwind CSS + CSS modules
  - Wallet: Auro Wallet integration for Mina transactions

  Key Components

  Pages Structure:
  - index.tsx - Landing page with navigation to auctions/creation
  - auctions.tsx - Live auctions listing with filtering/sorting
  - create.tsx - Auction creation form
  - bid/[id].tsx - Individual auction bidding page
  - auction-info/[id].tsx - Auction details page
  - finished-auctions.tsx - Completed auctions

  Core Features:
  1. Wallet Integration (useWallet.ts): Connects to Auro Wallet for Mina blockchain transactions
  2. ZkApp Workers: Background blockchain processing with zkappWorker.ts and zkappWorkerClient.ts
  3. Responsive UI: Mobile-first design with animated backgrounds and interactive elements
  4. Real-time Data: Fetches auction data from backend API endpoints

  Key Flows:
  1. Users connect Mina wallet via Auro
  2. Browse live auctions with sorting/filtering
  3. Register to bid or participate in live auctions
  4. Create new auctions with item details
  5. View completed auctions and results

  The app uses environment variables for backend API URLs and implements proper error handling throughout the user journey.    