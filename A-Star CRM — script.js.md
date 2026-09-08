```javascript
// ===============================
// A-STAR CRM
// Freight Forwarder CRM
// ===============================

let data = {
  customers: JSON.parse(localStorage.getItem("customers")) || [],
  enquiries: JSON.parse(localStorage.getItem("enquiries")) || [],
  quotations: JSON.parse(localStorage.getItem("quotations")) || [],
  shipments: JSON.parse(localStorage.getItem("shipments")) || [],
  followups: JSON.parse(localStorage.getItem("followups")) || []
};

let currentType = "";

document.addEventListener("DOMContentLoaded", () => {

  document.getElementById("today").textContent =
    new Date().toLocaleDateString("en-IN", {
      day: "2-digit",
      month: "short",
      year: "numeric"
    });

  document.querySelectorAll(".nav-btn").forEach(button => {
    button.addEventListener("click", () => {

      document.querySelectorAll(".nav-btn")
        .forEach(btn => btn.classList.remove("active"));

      document.querySelectorAll(".section")
        .forEach(section => section.classList.remove("active"));

      button.classList.add("active");

      const section = button.dataset.section;

      document.getElementById(section).classList.add("active");

      const title = section.charAt(0).toUpperCase() + section.slice(1);

      document.getElementById("pageTitle").textContent = title;
    });
  });

  renderAll();
});


// ===============================
// SAVE DATA
// ===============================

function saveData() {
  localStorage.setItem("customers", JSON.stringify(data.customers));
  localStorage.setItem("enquiries", JSON.stringify(data.enquiries));
  localStorage.setItem("quotations", JSON.stringify(data.quotations));
  localStorage.setItem("shipments", JSON.stringify(data.shipments));
  localStorage.setItem("followups", JSON.stringify(data.followups));
}


// ===============================
// MODAL
// ===============================

function openModal(type) {

  currentType = type;

  const modal = document.getElementById("modal");
  const form = document.getElementById("crmForm");
  const title = document.getElementById("modalTitle");

  modal.classList.add("show");

  let html = "";

  if (type === "customer") {

    title.textContent = "Add Customer";

    html = `
      <div class="form-grid">

        <div class="form-group">
          <label>Company Name</label>
          <input name="company" required>
        </div>

        <div class="form-group">
          <label>Contact Person</label>
          <input name="contact" required>
        </div>

        <div class="form-group">
          <label>Phone</label>
          <input name="phone">
        </div>

        <div class="form-group">
          <label>Email</label>
          <input name="email" type="email">
        </div>

        <div class="form-group">
          <label>City</label>
          <input name="city">
        </div>

        <div class="form-group">
          <label>Customer Type</label>
          <select name="type">
            <option>Exporter</option>
            <option>Importer</option>
            <option>Trader</option>
            <option>Manufacturer</option>
          </select>
        </div>

      </div>

      <button class="form-submit">Save Customer</button>
    `;
  }


  if (type === "enquiry") {

    title.textContent = "New Enquiry";

    html = `
      <div class="form-grid">

        <div class="form-group">
          <label>Customer</label>
          <input name="customer" required>
        </div>

        <div class="form-group">
          <label>Origin / POL</label>
          <input name="origin" placeholder="Nhava Sheva">
        </div>

        <div class="form-group">
          <label>Destination / POD</label>
          <input name="destination" placeholder="Santos">
        </div>

        <div class="form-group">
          <label>Equipment</label>
          <select name="equipment">
            <option>20 GP</option>
            <option>40 GP</option>
            <option>40 HC</option>
            <option>45 HC</option>
            <option>LCL</option>
          </select>
        </div>

        <div class="form-group full">
          <label>Commodity</label>
          <input name="commodity">
        </div>

        <div class="form-group">
          <label>Status</label>
          <select name="status">
            <option>New</option>
            <option>Quoted</option>
            <option>Won</option>
            <option>Lost</option>
          </select>
        </div>

      </div>

      <button class="form-submit">Save Enquiry</button>
    `;
  }


  if (type === "quotation") {

    title.textContent = "New Quotation";

    html = `
      <div class="form-grid">

        <div class="form-group">
          <label>Customer</label>
          <input name="customer" required>
        </div>

        <div class="form-group">
          <label>Route</label>
          <input name="route" placeholder="Nhava Sheva → Santos">
        </div>

        <div class="form-group">
          <label>Equipment</label>
          <select name="equipment">
            <option>20 GP</option>
            <option>40 GP</option>
            <option>40 HC</option>
            <option>LCL</option>
          </select>
        </div>

        <div class="form-group">
          <label>Freight Amount</label>
          <input name="freight" type="number">
        </div>

        <div class="form-group">
          <label>Currency</label>
          <select name="currency">
            <option>USD</option>
            <option>INR</option>
            <option>EUR</option>
          </select>
        </div>

        <div class="form-group">
          <label>Status</label>
          <select name="status">
            <option>Draft</option>
            <option>Sent</option>
            <option>Accepted</option>
            <option>Rejected</option>
          </select>
        </div>

      </div>

      <button class="form-submit">Save Quotation</button>
    `;
  }


  if (type === "shipment") {

    title.textContent = "New Shipment";

    html = `
      <div class="form-grid">

        <div class="form-group">
          <label>Booking Number</label>
          <input name="booking" required>
        </div>

        <div class="form-group">
          <label>Customer</label>
          <input name="customer">
        </div>

        <div class="form-group">
          <label>POL</label>
          <input name="pol" placeholder="Mundra">
        </div>

        <div class="form-group">
          <label>POD</label>
          <input name="pod" placeholder="Durban">
        </div>

        <div class="form-group">
          <label>Vessel</label>
          <input name="vessel">
        </div>

        <div class="form-group">
          <label>Status</label>
          <select name="status">
            <option>Booking Confirmed</option>
            <option>Container Picked Up</option>
            <option>Gate In</option>
            <option>Loaded</option>
            <option>In Transit</option>
            <option>Arrived</option>
            <option>Delivered</option>
          </select>
        </div>

      </div>

      <button class="form-submit">Save Shipment</button>
    `;
  }


  if (type === "followup") {

    title.textContent = "Add Follow-up";

    html = `
      <div class="form-grid">

        <div class="form-group">
          <label>Customer</label>
          <input name="customer" required>
        </div>

        <div class="form-group">
          <label>Follow-up Date</label>
          <input name="date" type="date" required>
        </div>

        <div class="form-group full">
          <label>Notes</label>
          <textarea name="notes"></textarea>
        </div>

        <div class="form-group">
          <label>Status</label>
          <select name="status">
            <option>Pending</option>
            <option>Completed</option>
          </select>
        </div>

      </div>

      <button class="form-submit">Save Follow-up</button>
    `;
  }

  form.innerHTML = html;

  form.onsubmit = function(event) {
    event.preventDefault();

    const formData = new FormData(form);
    const item = Object.fromEntries(formData.entries());

    item.id = Date.now();

    data[currentType + "s"].push(item);

    saveData();

    closeModal();
    renderAll();

    alert("Saved successfully!");
  };
}


function closeModal() {
  document.getElementById("modal").classList.remove("show");
}


// ===============================
// CUSTOMERS
// ===============================

function renderCustomers() {

  const table = document.getElementById("customerTable");
  const search = document.getElementById("customerSearch").value.toLowerCase();

  table.innerHTML = "";

  const filtered = data.customers.filter(customer =>
    `${customer.company} ${customer.contact} ${customer.city}`
      .toLowerCase()
      .includes(search)
  );

  if (filtered.length === 0) {
    table.innerHTML = `
      <tr>
        <td colspan="6" class="empty">No customers found.</td>
      </tr>
    `;
    return;
  }

  filtered.forEach(customer => {

    table.innerHTML += `
      <tr>
        <td>${customer.company}</td>
        <td>${customer.contact}</td>
        <td>${customer.phone || "-"}</td>
        <td>${customer.email || "-"}</td>
        <td>${customer.city || "-"}</td>
        <td>
          <button class="action-btn"
            onclick="deleteRecord('customers', ${customer.id})">
            Delete
          </button>
        </td>
      </tr>
    `;
  });
}


// ===============================
// ENQUIRIES
// ===============================

function renderEnquiries() {

  const table = document.getElementById("enquiryTable");

  table.innerHTML = "";

  if (data.enquiries.length === 0) {

    table.innerHTML = `
      <tr>
        <td colspan="7" class="empty">No enquiries found.</td>
      </tr>
    `;

    return;
  }

  data.enquiries.forEach(item => {

    table.innerHTML += `
      <tr>
        <td>${item.customer}</td>
        <td>${item.origin}</td>
        <td>${item.destination}</td>
        <td>${item.equipment}</td>
        <td>${item.commodity}</td>
        <td>${item.status}</td>
        <td>
          <button class="action-btn"
          onclick="deleteRecord('enquiries', ${item.id})">
          Delete
          </button>
        </td>
      </tr>
    `;
  });
}


// ===============================
// QUOTATIONS
// ===============================

function renderQuotations() {

  const table = document.getElementById("quotationTable");

  table.innerHTML = "";

  if (data.quotations.length === 0) {

    table.innerHTML = `
      <tr>
        <td colspan="7" class="empty">No quotations found.</td>
      </tr>
    `;

    return;
  }

  data.quotations.forEach(item => {

    table.innerHTML += `
      <tr>
        <td>${item.customer}</td>
        <td>${item.route}</td>
        <td>${item.equipment}</td>
        <td>${item.freight}</td>
        <td>${item.currency}</td>
        <td>${item.status}</td>
        <td>
          <button class="action-btn"
          onclick="deleteRecord('quotations', ${item.id})">
          Delete
          </button>
        </td>
      </tr>
    `;
  });
}


// ===============================
// SHIPMENTS
// ===============================

function renderShipments() {

  const table = document.getElementById("shipmentTable");

  table.innerHTML = "";

  if (data.shipments.length === 0) {

    table.innerHTML = `
      <tr>
        <td colspan="7" class="empty">No shipments found.</td>
      </tr>
    `;

    return;
  }

  data.shipments.forEach(item => {

    table.innerHTML += `
      <tr>
        <td>${item.booking}</td>
        <td>${item.customer}</td>
        <td>${item.pol}</td>
        <td>${item.pod}</td>
        <td>${item.vessel}</td>
        <td>${item.status}</td>
        <td>
          <button class="action-btn"
          onclick="deleteRecord('shipments', ${item.id})">
          Delete
          </button>
        </td>
      </tr>
    `;
  });
}


// ===============================
// FOLLOW UPS
// ===============================

function renderFollowups() {

  const table = document.getElementById("followupTable");

  table.innerHTML = "";

  if (data.followups.length === 0) {

    table.innerHTML = `
      <tr>
        <td colspan="5" class="empty">No follow-ups found.</td>
      </tr>
    `;

    return;
  }

  data.followups.forEach(item => {

    table.innerHTML += `
      <tr>
        <td>${item.customer}</td>
        <td>${item.date}</td>
        <td>${item.notes}</td>
        <td>${item.status}</td>
        <td>
          <button class="action-btn"
          onclick="deleteRecord('followups', ${item.id})">
          Delete
          </button>
        </td>
      </tr>
    `;
  });
}


// ===============================
// DELETE
// ===============================

function deleteRecord(type, id) {

  if (!confirm("Are you sure you want to delete this record?")) {
    return;
  }

  data[type] = data[type].filter(item => item.id !== id);

  saveData();

  renderAll();
}


// ===============================
// DASHBOARD
// ===============================

function updateDashboard() {

  document.getElementById("customerCount").textContent =
    data.customers.length;

  document.getElementById("enquiryCount").textContent =
    data.enquiries.filter(item => item.status !== "Lost").length;

  document.getElementById("quotationCount").textContent =
    data.quotations.length;

  document.getElementById("shipmentCount").textContent =
    data.shipments.filter(item =>
      item.status !== "Delivered"
    ).length;

  const activity = document.getElementById("recentActivity");

  const all = [
    ...data.customers.map(x => ({
      text: `Customer added: ${x.company}`,
      id: x.id
    })),
    ...data.enquiries.map(x => ({
      text: `Enquiry: ${x.origin} → ${x.destination}`,
      id: x.id
    })),
    ...data.shipments.map(x => ({
      text: `Shipment: ${x.booking}`,
      id: x.id
    }))
  ]
  .sort((a,b) => b.id - a.id)
  .slice(0,5);

  if (all.length === 0) {
    activity.innerHTML = "No activity yet.";
  } else {
    activity.innerHTML = all
      .map(item => `<p>${item.text}</p>`)
      .join("");
  }
}


// ===============================
// RENDER EVERYTHING
// ===============================

function renderAll() {

  renderCustomers();
  renderEnquiries();
  renderQuotations();
  renderShipments();
  renderFollowups();
  updateDashboard();
}
```