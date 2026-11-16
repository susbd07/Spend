A personal expense tracker that runs on your phone like a native app. Built for everyday use in Bangladesh, with BDT as the default currency.

Live app: https://susbd07.github.io/Spend/

Spend is a Progressive Web App (PWA). It is a single HTML page with no server and no sign-up. Your personal data stays on your own device.

Features

Everyday tracking

	•	Add expenses and income with a category, note, date and payment method (Cash, bKash, Nagad, Rocket, Bank, Card)
	•	Categories suited to Bangladesh, including Groceries, Rent, Bills, Mobile & net, and Zakat, Pujo & donation
	•	Monthly overview with income, spending, balance and a category breakdown
	•	Monthly budgets per category, with warnings at 80% and 100%
	•	Alerts when spending on categories you mark as non-essential grows fast

Reviews and trends

	•	Weekly review (weeks run Saturday to Friday) with a written summary, daily chart and comparison with last week
	•	Six-month trend of spending versus income

Currencies

	•	BDT by default, plus USD and one custom currency of your choice (any code, symbol and rate)
	•	Live exchange rates with one tap, or type rates by hand
	•	Lakh/crore number grouping and an optional Bangla digits mode

Money

	•	Loans: money you lent or borrowed, with due dates, part payments and overdue flags
	•	Investments: DPS, FDR, Sanchayapatra, stocks, gold, crypto and more, with gain or loss
	•	Trip history: every completed trip and the amount deducted from your main account

Trips

	•	Create a trip, add shared expenses with a category and comment, and split them equally or by custom amounts
	•	See who owes whom and mark settlements as paid
	•	Share a trip with a code so friends can join and add expenses from their own phones
	•	Complete a trip to deduct your share from your main account in one entry, with full expense details saved in Trip history

Everything else

	•	Light, dark or automatic theme with soft colour palettes
	•	Works offline once opened
	•	Export to CSV, back up and restore (file or copied text)

Install on your phone

iPhone (Safari)

	1.	Open the live app link in Safari.
	2.	Tap Share, then Add to Home Screen, then Add.
	3.	Open the app from the home-screen icon from then on.

Android (Chrome)

	1.	Open the live app link in Chrome.
	2.	Tap the menu (three dots), then Install app or Add to Home screen.

The home-screen app and the browser keep separate data, so use one consistently.

Your data

	•	Personal expenses, loans, investments and settings are stored on your device only.
	•	Back up regularly from Settings > Your data. Clearing browser data or removing the app deletes your entries unless you have a backup.
	•	Shared trips are stored in a Firebase Firestore database so that everyone on a trip sees the same data. Anyone who knows a trip code can open that trip, so share codes only with people you trust.
	•	Visit counts are collected with GoatCounter, which does not use cookies and does not see your expenses.

Run your own copy

	1.	Fork this repository and enable GitHub Pages (Settings > Pages > deploy from the main branch, root folder).
	2.	For trip sharing, create a Firebase project with a Firestore database and these rules:

rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /trips/{code} {
      allow get: if true;
      allow create, update: if request.resource.data.keys().hasOnly(['data'])
        && request.resource.data.data is string
        && request.resource.data.data.size() < 200000;
      allow list, delete: if false;
    }
  }
}

	3.	In index.html, replace the Firebase project ID and web API key with your own (search for spend-tracker-git).
	4.	Restrict your API key to your site address in Google Cloud Console, and use the Firebase Spark (free) plan.
	5.	To use your own analytics, replace the GoatCounter script in index.html, or remove it.

Files

File	Purpose
index.html	The whole app: layout, styles and code
sw.js	Service worker that lets the app work offline

Tech

Plain HTML, CSS and JavaScript with no build step and no dependencies. Data is kept in the browser's local storage. Trip sharing uses the Firestore REST API.
