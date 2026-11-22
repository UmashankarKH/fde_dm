# Setup 02: Azure (optional, but recommended for the cloud part)

**Goal:** create a cloud storage account where you can put your cleaned data and your helpers' logs.

**Who needs this:** teams who want to show the cloud version. Teams who work fully on a laptop can skip it. The assignment says Azure is optional, and you lose no marks for skipping it.

**Time needed:** about 60 minutes the first time.

---

## Before you start

- **Use a personal account, not a client's account.** Never use real client data here.
- **Check the current free offer.** Azure's free account terms change. Look at https://azure.microsoft.com/free before you sign up, and read what is free and for how long.
- **Set a budget alert before you create anything.** This protects you from surprise bills.

---

## Step 1: Create a free account and a budget alert

1. Go to https://azure.microsoft.com/free and sign up. You need a phone number and a card for identity checks.
2. Sign in to the **Azure Portal** at https://portal.azure.com.
3. In the top search bar, type **Cost Management + Billing** and open it. (If your account shows several billing scopes, choose the one that belongs to your free subscription.)
4. Go to **Budgets**, click **+ Add**, and set:
   - **Amount:** a small monthly amount your trainer recommends
   - **Alerts:** at 50% and 90% of the budget, sent to your email
5. Click **Create**.

---

## Step 2: Create a resource group

A resource group is one folder for everything in this project. Deleting the folder deletes everything in it.

1. Search for **Resource groups**, then click **+ Create**.
2. Fill in:
   - **Subscription:** your subscription
   - **Resource group name:** `rg-kaveri-yourname`
   - **Region:** a region close to you (for example, **Central India** or **East US**)
3. Click **Review + create**, then **Create**.

---

## Step 3: Create a storage account for your data

1. Search for **Storage accounts**, then click **+ Create**.
2. **Basics** tab:
   - **Resource group:** `rg-kaveri-yourname`
   - **Storage account name:** lowercase letters and numbers only, unique worldwide, for example `kaveriyourname01`
   - **Region:** the same as your resource group
   - **Performance:** Standard
   - **Redundancy:** LRS (cheapest)
3. **Advanced** tab: turn on **Enable hierarchical namespace**. This turns the storage into a data lake.
4. Click **Review + create**, then **Create**. When it finishes, click **Go to resource**.
5. In the left menu, open **Containers** and create two containers:
   - `raw` (for the untouched CSV files)
   - `clean` (for your cleaned data and your helpers' logs)

---

## Step 4: Upload your raw files

1. Open the `raw` container.
2. Click **Upload**, select your four team folders' CSV files, and click **Upload**.

Only upload the **dummy** data from `data_learners/`. Never upload real client data.

---

## Step 5: Use the cloud storage from your code (optional)

When you're ready to read the files from Python, use **managed identity** or a key from Key Vault. Never paste the storage key into your code or your repository.

Ask your trainer for the current recommended library and sign-in method, because these change.

---

## Step 6: Clean up when you are finished

1. Open **Resource groups**, click `rg-kaveri-yourname`, and click **Delete resource group**.
2. Type the name to confirm, then click **Delete**.

Do this at the end of the assignment, or when you have submitted, so nothing keeps charging.

---

## Common problems

| Problem | Fix |
|---|---|
| "Storage account name is taken" | Add more numbers or letters to the name |
| Hierarchical namespace option missing | Choose the storage type **Azure Blob Storage or Azure Data Lake Storage** on the Basics tab, then retry the Advanced tab |
| Costs are higher than expected | Check **Cost Management**. Delete resources you are not using |
| Cannot sign in | Use a private browser window. Check that your account is not locked |
