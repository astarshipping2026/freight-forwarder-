```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>A-Star Shipping & Logistics CRM</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

<div class="app">

  <aside class="sidebar">
    <div class="logo">
      <div class="logo-circle">A</div>
      <div>
        <h2>A-STAR</h2>
        <span>Shipping & Logistics</span>
      </div>
    </div>

    <nav>
      <button class="nav-btn active" data-section="dashboard">📊 Dashboard</button>
      <button class="nav-btn" data-section="customers">👥 Customers</button>
      <button class="nav-btn" data-section="enquiries">📩 Enquiries</button>
      <button class="nav-btn" data-section="quotations">💰 Quotations</button>
      <button class="nav-btn" data-section="shipments">🚢 Shipments</button>
      <button class="nav-btn" data-section="followups">📞 Follow-ups</button>
    </nav>

    <div class="sidebar-bottom">
      <span>A-Star CRM</span>
      <small>Freight Forwarding Management</small>
    </div>
  </aside>

  <main class="main">

    <header class="topbar">
      <div>
        <h1 id="pageTitle">Dashboard</h1>
        <p>Welcome to A-Star Shipping & Logistics CRM</p>
      </div>
      <div class="today" id="today"></div>
    </header>

    <!-- DASHBOARD -->
    <section id="dashboard" class="section active">
      <div class="cards">
        <div class="card">
          <span>Total Customers</span>
          <strong id="customerCount">0</strong>
        </div>
        <div class="card">
          <span>Open Enquiries</span>
          <strong id="enquiryCount">0</strong>
        </div>
        <div class="card">
          <span>Quotations</span>
          <strong id="quotationCount">0</strong>
        </div>
        <div class="card">
          <span>Active Shipments</span>
          <strong id="shipmentCount">0</strong>
        </div>
      </div>

      <div class="panel">
        <h2>Quick Actions</h2>
        <div class="quick-actions">
          <button onclick="openModal('customer')">+ Add Customer</button>
          <button onclick="openModal('enquiry')">+ New Enquiry</button>
          <button onclick="openModal('quotation')">+ New Quotation</button>
          <button onclick="openModal('shipment')">+ New Shipment</button>
        </div>
      </div>

      <div class="panel">
        <h2>Recent Activity</h2>
        <div id="recentActivity" class="empty">No activity yet.</div>
      </div>
    </section>

    <!-- CUSTOMERS -->
    <section id="customers" class="section">
      <div class="section-head">
        <div>
          <h2>Customers</h2>
          <p>Manage your clients and contacts.</p>
        </div>
        <button class="primary" onclick="openModal('customer')">+ Add Customer</button>
      </div>

      <input class="search" id="customerSearch" placeholder="Search customers..." oninput="renderCustomers()">

      <div class="table-container">
        <table>
          <thead>
            <tr>
              <th>Company</th>
              <th>Contact Person</th>
              <th>Phone</th>
              <th>Email</th>
              <th>City</th>
              <th>Action</th>
            </tr>
          </thead>
          <tbody id="customerTable"></tbody>
        </table>
      </div>
    </section>

    <!-- ENQUIRIES -->
    <section id="enquiries" class="section">
      <div class="section-head">
        <div>
          <h2>Enquiries</h2>
          <p>Track incoming freight enquiries.</p>
        </div>
        <button class="primary" onclick="openModal('enquiry')">+ New Enquiry</button>
      </div>

      <div class="table-container">
        <table>
          <thead>
            <tr>
              <th>Customer</th>
              <th>Origin</th>
              <th>Destination</th>
              <th>Equipment</th>
              <th>Commodity</th>
              <th>Status</th>
              <th>Action</th>
            </tr>
          </thead>
          <tbody id="enquiryTable"></tbody>
        </table>
      </div>
    </section>

    <!-- QUOTATIONS -->
    <section id="quotations" class="section">
      <div class="section-head">
        <div>
          <h2>Quotations</h2>
          <p>Manage freight quotations.</p>
        </div>
        <button class="primary" onclick="openModal('quotation')">+ New Quotation</button>
      </div>

      <div class="table-container">
        <table>
          <thead>
            <tr>
              <th>Customer</th>
              <th>Route</th>
              <th>Equipment</th>
              <th>Freight</th>
              <th>Currency</th>
              <th>Status</th>
              <th>Action</th>
            </tr>
          </thead>
          <tbody id="quotationTable"></tbody>
        </table>
      </div>
    </section>

    <!-- SHIPMENTS -->
    <section id="shipments" class="section">
      <div class="section-head">
        <div>
          <h2>Shipments</h2>
          <p>Track your active shipments.</p>
        </div>
        <button class="primary" onclick="openModal('shipment')">+ New Shipment</button>
      </div>

      <div class="table-container">
        <table>
          <thead>
            <tr>
              <th>Booking No.</th>
              <th>Customer</th>
              <th>POL</th>
              <th>POD</th>
              <th>Vessel</th>
              <th>Status</th>
              <th>Action</th>
            </tr>
          </thead>
          <tbody id="shipmentTable"></tbody>
        </table>
      </div>
    </section>

    <!-- FOLLOW UPS -->
    <section id="followups" class="section">
      <div class="section-head">
        <div>
          <h2>Follow-ups</h2>
          <p>Keep track of customer follow-ups.</p>
        </div>
        <button class="primary" onclick="openModal('followup')">+ Add Follow-up</button>
      </div>

      <div class="table-container">
        <table>
          <thead>
            <tr>
              <th>Customer</th>
              <th>Follow-up Date</th>
              <th>Notes</th>
              <th>Status</th>
              <th>Action</th>
            </tr>
          </thead>
          <tbody id="followupTable"></tbody>
        </table>
      </div>
    </section>

  </main>
</div>

<!-- MODAL -->
<div id="modal" class="modal">
  <div class="modal-box">
    <div class="modal-header">
      <h2 id="modalTitle">Add</h2>
      <button onclick="closeModal()">×</button>
    </div>

    <form id="crmForm"></form>
  </div>
</div>

<script src="script.js"></script>
</body>
</html>
```