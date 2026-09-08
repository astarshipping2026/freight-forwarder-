```css
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: Arial, sans-serif;
}

body {
  background: #f4f6f8;
  color: #222;
}

.app {
  display: flex;
  min-height: 100vh;
}

/* SIDEBAR */

.sidebar {
  width: 250px;
  background: #111827;
  color: white;
  padding: 22px 15px;
  position: fixed;
  height: 100vh;
  left: 0;
  top: 0;
}

.logo {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 5px 8px 25px;
}

.logo-circle {
  width: 45px;
  height: 45px;
  background: #dc2626;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 25px;
  font-weight: bold;
}

.logo h2 {
  font-size: 18px;
}

.logo span {
  font-size: 10px;
  color: #d1d5db;
}

nav {
  display: flex;
  flex-direction: column;
  gap: 7px;
}

.nav-btn {
  border: none;
  background: transparent;
  color: #d1d5db;
  padding: 13px;
  text-align: left;
  border-radius: 7px;
  cursor: pointer;
  font-size: 14px;
}

.nav-btn:hover,
.nav-btn.active {
  background: #dc2626;
  color: white;
}

.sidebar-bottom {
  position: absolute;
  bottom: 25px;
  left: 20px;
  right: 20px;
  color: #9ca3af;
}

.sidebar-bottom small {
  display: block;
  margin-top: 5px;
}

/* MAIN */

.main {
  margin-left: 250px;
  width: calc(100% - 250px);
  padding: 30px;
}

.topbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 25px;
}

.topbar h1 {
  font-size: 28px;
}

.topbar p {
  color: #6b7280;
  margin-top: 5px;
}

.today {
  color: #6b7280;
}

/* SECTIONS */

.section {
  display: none;
}

.section.active {
  display: block;
}

/* CARDS */

.cards {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 18px;
  margin-bottom: 25px;
}

.card {
  background: white;
  padding: 22px;
  border-radius: 10px;
  box-shadow: 0 2px 8px rgba(0,0,0,.06);
}

.card span {
  color: #6b7280;
  font-size: 14px;
}

.card strong {
  display: block;
  font-size: 30px;
  margin-top: 10px;
}

/* PANEL */

.panel {
  background: white;
  padding: 22px;
  border-radius: 10px;
  margin-bottom: 20px;
}

.panel h2 {
  margin-bottom: 15px;
}

/* BUTTONS */

button {
  cursor: pointer;
}

.primary,
.quick-actions button {
  border: none;
  background: #dc2626;
  color: white;
  padding: 11px 17px;
  border-radius: 6px;
  cursor: pointer;
}

.primary:hover,
.quick-actions button:hover {
  background: #b91c1c;
}

.quick-actions {
  display: flex;
  gap: 10px;
  flex-wrap: wrap;
}

/* SECTION HEADER */

.section-head {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 18px;
}

.section-head p {
  color: #6b7280;
  margin-top: 5px;
}

/* SEARCH */

.search {
  width: 100%;
  padding: 12px;
  border: 1px solid #ddd;
  border-radius: 7px;
  margin-bottom: 15px;
}

/* TABLE */

.table-container {
  background: white;
  border-radius: 10px;
  overflow-x: auto;
  box-shadow: 0 2px 8px rgba(0,0,0,.05);
}

table {
  width: 100%;
  border-collapse: collapse;
}

th,
td {
  padding: 14px;
  text-align: left;
  border-bottom: 1px solid #eee;
  font-size: 14px;
}

th {
  background: #f9fafb;
  color: #374151;
}

.action-btn {
  border: none;
  background: #fee2e2;
  color: #b91c1c;
  padding: 7px 10px;
  border-radius: 5px;
}

/* MODAL */

.modal {
  display: none;
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,.5);
  align-items: center;
  justify-content: center;
  padding: 20px;
  z-index: 100;
}

.modal.show {
  display: flex;
}

.modal-box {
  width: 600px;
  max-width: 100%;
  max-height: 90vh;
  overflow-y: auto;
  background: white;
  border-radius: 10px;
  padding: 22px;
}

.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}

.modal-header button {
  border: none;
  background: transparent;
  font-size: 28px;
}

.form-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 15px;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.form-group.full {
  grid-column: 1 / -1;
}

.form-group input,
.form-group select,
.form-group textarea {
  padding: 11px;
  border: 1px solid #ddd;
  border-radius: 6px;
}

.form-group textarea {
  min-height: 90px;
  resize: vertical;
}

.form-submit {
  margin-top: 20px;
  width: 100%;
  border: none;
  background: #dc2626;
  color: white;
  padding: 13px;
  border-radius: 6px;
  font-size: 15px;
}

/* MOBILE */

@media (max-width: 900px) {
  .sidebar {
    width: 210px;
  }

  .main {
    margin-left: 210px;
    width: calc(100% - 210px);
  }

  .cards {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 650px) {
  .sidebar {
    position: relative;
    width: 100%;
    height: auto;
  }

  .app {
    display: block;
  }

  .main {
    margin-left: 0;
    width: 100%;
    padding: 15px;
  }

  .cards {
    grid-template-columns: 1fr;
  }

  .form-grid {
    grid-template-columns: 1fr;
  }

  .topbar {
    display: block;
  }

  .today {
    margin-top: 10px;
  }
}
```