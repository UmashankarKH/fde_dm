# Client Discovery Call: Kaveri Kitchen Supplies Pvt Ltd

**Type:** Dummy transcript for the learner assignment. All companies and people are fictional.
**Length:** about 45 minutes, reconstructed for training
**Your role:** Forward Deployed Engineer (FDE) at Chennaya Technologies. You are the consultant on this call.

## Who is on the call

| Name | Role |
|---|---|
| You (the FDE) | Forward Deployed Engineer, Chennaya Technologies |
| Meera Nair | Head of Operations, Kaveri Kitchen Supplies |
| Rahul Verma | Sales Manager (owns the CRM and order process) |
| Dinesh Kumar | Warehouse Lead (owns stock and deliveries) |
| Pooja Iyer | Finance Controller (owns invoices and GST) |
| Asha Menon | Customer Service Lead (owns returns and complaints) |

Kaveri Kitchen Supplies is a distributor. It buys kitchen appliances and utensils from manufacturers and sells them to hotels, caterers, cafes, shops and hostels across the state. It has about 90 employees and 12 key B2B customers in this pilot.

---

## Scene 1: The problem as the client sees it

**Meera Nair:** Thanks for coming in. I'll be direct. We have a problem that costs us money every week, and nobody can see the whole picture.

**You:** Thanks, Meera. Before we go further, can you walk me through what happens when a customer places an order?

**Meera Nair:** Rahul takes the order, usually by email or phone. He enters it in his CRM. Then the warehouse ships it. Then Pooja's team raises an invoice. Each step works on its own. The problem is between the steps.

**You:** Which problem shows up most often?

**Meera Nair:** Overselling. Rahul promises a customer a product that Dinesh doesn't actually have on the shelf. The customer gets a delay, and Rahul looks bad. Last month we had eleven orders where we confirmed stock that wasn't there.

**Rahul Verma:** To be fair, I check the stock. I just check the sheet Dinesh sends me on Monday. By Wednesday it's wrong.

**Dinesh Kumar:** My system is updated every time something goes out. Rahul doesn't have access to it. He has a copy from Monday.

**You:** So the sales side and the warehouse side are looking at different versions of stock?

**Dinesh Kumar:** Yes. And I don't send Rahul the live data. Our policy is that each team keeps its own system.

---

## Scene 2: What each team actually uses

**You:** Let's go through the systems one by one. Pooja, what do you use for invoices?

**Pooja Iyer:** An accounting package. We export invoices to a spreadsheet every Friday, and I reconcile them by hand. Each invoice has a customer code, like CUST-101, and an invoice number. The invoice does not have the sales order number on it. We never added that field.

**You:** So if I have an invoice, I can't tell which sales order it came from?

**Pooja Iyer:** Not directly. I match by customer and product, and I check the quantities against the delivery note.

**You:** And Asha, what do you use for returns?

**Asha Menon:** A shared sheet and our email inbox. Customers write in with a complaint, and my team logs a return. Customers mostly give their email address, not a customer code. Sometimes they give the order number, sometimes they don't. The order number is in the format SO-1001 for sales, but the warehouse writes it as SO1001 with no dash, so people mix them up.

**Dinesh Kumar:** I use a warehouse management tool. Every product has a SKU code like KK-001. Stock in, stock out, deliveries. The order reference is whatever the sales team gives me, which is usually the sales order number.

**Rahul Verma:** My CRM stores the product as a name, like "Pressure Cooker 5L". I don't record the SKU. My customers don't know the SKU codes.

---

## Scene 3: The data model question

**You:** Do you have an entity relationship diagram, or a data model that shows how these tables connect?

**Meera Nair:** Nothing. Our IT vendor set up the systems in 2021 and left in 2023. We never had a diagram.

**You:** So nobody has written down how a customer, an order, a delivery, an invoice and a return relate to each other?

**Pooja Iyer:** Everyone has a version in their head. Mine is different from Rahul's.

**You:** That's useful to know. It means we have to design the connections ourselves before we can automate anything.

**Meera Nair:** That sounds like a lot of work.

**You:** It's the first two weeks of work, and it's what makes the rest of the project reliable. Without it, the automation would guess which invoice belongs to which order, and it would guess wrong.

---

## Scene 4: Teams do not see each other's data

**You:** Can Rahul see the warehouse stock directly, live?

**Meera Nair:** No. That's a deliberate rule, and it's sensible. The warehouse data is commercially sensitive, and sales should not be able to change it. Each team owns its own data.

**You:** So any solution has to respect that. We can't just combine everything into one shared database and give everyone access.

**Meera Nair:** Right. But I still need the problems solved. Can you do both?

**You:** We can design it so each team keeps its own data, and a separate process reads only the fields it needs to answer a specific question. Pooja, if the agent needs to know whether an invoice matches a delivery, which fields does it need, and which ones should it never see?

**Pooja Iyer:** It needs the invoice number, the product, the billed quantity and the customer. It doesn't need bank details or the salary of anyone.

**Asha Menon:** And customer emails. Legal says we can't send customer emails to outside tools without masking them.

**You:** Good. That's a rule we will build into the design. Personal details get masked before any AI tool sees them.

---

## Scene 5: The pain, in numbers

**You:** Let's get specific. Can you estimate how many times each problem happens in a normal week?

**Meera Nair:** Overselling is about two orders a week. Some weeks it's four.

**Pooja Iyer:** Invoice mismatches, where we billed more than we delivered, are the big one. I'd say one in eight invoices needs a manual check. That's about ten a week. It takes me two days every Friday.

**Asha Menon:** Returns. About fifteen a week. Roughly a third of them have no order number, so I spend time searching the sales sheet by email address.

**You:** So the overall cost is roughly Pooja's two days, Asha's time on lost returns, and the customer goodwill when Rahul has to apologise for a delayed order?

**Meera Nair:** Yes. And I'd add that customers have started to notice. Two of our biggest hotel clients asked why their invoices don't match their delivery notes.

**You:** That's a risk I'd want to fix first.

---

## Scene 6: What the client wants automated

**Meera Nair:** I'd like the process to stop guessing. Here's my wish list. One: before Rahul confirms an order, something checks whether the stock is really there, with live numbers. Two: before an invoice goes out, something checks that what we bill matches what we delivered. Three: when a customer writes about a return, we can find their order fast.

**You:** Which one matters most?

**Meera Nair:** The first one. If we stop overselling, we stop most of the other problems.

**You:** Here's what I'd suggest. We don't have to automate everything in two weeks. We need to pick one problem, build a clear data model for it, and build a small team of AI helpers that handle it end to end. The rest comes after.

**Meera Nair:** Which problem would you pick?

**You:** The one that protects revenue and reputation. Overselling and invoice mismatches share the same root cause: the sales order, the delivery and the invoice are not linked. So the design work solves both.

**Dinesh Kumar:** I'd be happy with that, as long as the warehouse stays in control of its data.

**You:** Agreed. The warehouse data stays in the warehouse. The helpers read only what they need.

---

## Scene 7: Rules and constraints

**Pooja Iyer:** The invoices must follow GST rules. The agent can flag things, but it must never change an invoice on its own.

**Asha Menon:** Customers must not be contacted by an AI without a person approving the message.

**Meera Nair:** And I want to see the reasoning. If the system says an order is oversold, I want to see which stock figure it used, and when.

**You:** Those are good rules, and they fit the design. Three principles:
1. Every decision the AI makes is logged with the evidence it used.
2. A person approves anything that changes money, stock or a customer message.
3. Personal details are masked before an AI tool reads them.

**Meera Nair:** That's what I need.

---

## Scene 8: What the pilot should deliver

**You:** Here is what I'd propose for the pilot, in three weeks:
- A data model for the four teams' data, drawn on dbdiagram.io, with a short note on each table and key.
- Working queries that link a sales order to its delivery and its invoice, with the shared key rules written down.
- At least one AI helper team that does a real check. For example, a stock check before an order is confirmed, or an invoice-to-delivery match. The helpers must write their reasoning to a log.
- A short demo for Meera and her team, and a handover note they can read without you.

**Meera Nair:** Three weeks is tight. What if the data is messy?

**You:** It will be messy. That's the normal case. Part of the job is to write down what's messy and decide how to handle it. A clear list of problems is also a deliverable.

**Meera Nair:** Fine. Send me the plan by Friday. Pooja and Dinesh, please send the sample exports you've already shared with us, so the team can start the model.

**You:** I'll also ask for one thing from each team: a short list of the fields you use every day, and what each one means in your own words.

---

## Scene 9: Closing

**Meera Nair:** One last question. How do you know the AI won't make things worse?

**You:** Two ways. First, the rules that decide a match or a mismatch are written in code and tested, not left to the AI to guess. Second, the AI explains its answer, and a person signs off on anything that touches money or customers. If the AI is wrong, you'll see it in the log, and we fix the rule.

**Meera Nair:** Good. That's the answer I wanted.

**You:** Thank you, Meera. I'll send the plan by Friday.

---

## Notes for the learner (read before you start)

- Each team's data is separate. You won't find a shared key between teams. You have to build the links yourself.
- The customer identity problem is real: Sales uses email, Finance uses a customer code, and the names don't always match exactly.
- Order numbers are written two ways (SO-1001 and SO1001). Decide how to standardise them, and write the rule down.
- Personal data (customer emails) must be masked before any AI tool sees it.
- The AI helpers must never approve or change money, stock, or a customer message on their own.
