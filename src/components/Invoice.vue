<template>
    <div class="invoice">
      <div class="invoice-header">
        <div class="company-logo">
          <!-- Replace with your logo -->
          <img  alt="Company Logo" />
        </div>
        <div class="company-info">
          <h1>Invoice</h1>
          <p>Your Company Name</p>
          <p>Your Business Address</p>
          <p>City, Country, Postal</p>
        </div>
      </div>
      <div class="invoice-details">
        <div class="bill-to">
          <p><strong>Bill To:</strong></p>
          <p>Company Name</p>
          <p>Address</p>
          <p>City, Country, Postal</p>
        </div>
        <div class="invoice-info">
          <p><strong>Invoice #:</strong> <input type="text" ></p>
          <p><strong>Date:</strong> <input type="date" ></p>
          <p><strong>Invoice Due Date:</strong> <input type="date" ></p>
        </div>
      </div>
      <table class="invoice-table">
        <thead>
          <tr>
            <th>Items</th>
            <th>Description</th>
            <th>Quantity</th>
            <th>Price</th>
            <!-- <th>Tax</th> -->
            <th>Amount</th>
            <th>Action</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in items" :key="index">
            <td><input v-model="item.name" placeholder="Item Name"  /></td>
            <td><input v-model="item.description" placeholder="Description" /></td>
            <td><input type="number" v-model="item.quantity" placeholder="Quantity"  /></td>
            <td><input type="number" v-model="item.price" placeholder="Price" /></td>
            <!-- <td><input type="number" v-model="item.tax" placeholder="Tax" /></td> -->
            <td>{{ calculateAmount(item)}}</td>
            <td><button @click="removeItem(index)">Remove</button></td>
          </tr>
        </tbody>
      </table>
      <button @click="addItem">Add Item</button>
      
      <div class="notes">
        <p><strong>Notes:</strong></p>
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Praesent ut nisi tempus massa blandit luctus.</p>
      </div>
      <div class="total">
        <p><strong>Total:</strong> {{ calculateTotal() }}</p>
        
      </div>
      <div class="footer">
        <p>Powered by Wave</p>
        <p>This invoice was generated with the help of Wave Financial Inc.</p>
        <p>To learn more, and create your own free account visit waveapps.com</p>
      </div>
      <button @click="downloadinvoice">Download Invoice</button>  
    </div>
  </template>
  
  <script>
  export default {
    name: 'Invoice',
    data() {
      return {
        items: [
          {
            name: 'Item 1',
            description: 'Description',
            quantity: 1,
            price: 0,
            tax: 0
          }
        ]
      }
    },
    methods: {
      addItem() {
        this.items.push({
          name: '',
          description: '',
          quantity: 1,
          price: 0,
          
        });
      },
      removeItem(index) {
        this.items.splice(index, 1);
      },
      calculateAmount(item) {
        return (item.quantity * item.price).toFixed(2);
      },
      calculateTotal() {
        return this.items.reduce((total, item) => {
          return total + parseFloat(this.calculateAmount(item));
        }, 0).toFixed(2);
      }
    }
  }
  </script>
  
  <style scoped>
  .invoice {
    font-family: Arial, sans-serif;
  }
  
  .invoice-header {
    display: flex;
    justify-content: space-between;
    border-bottom: 2px solid #ccc;
    padding-bottom: 10px;
  }
  
  .company-logo img {
    max-width: 100px;
  }
  
  .company-info h1 {
    margin: 0;
  }
  
  .invoice-details {
    display: flex;
    justify-content: space-between;
      
  }
  
  .invoice-table {
    width: 100%;
    border-collapse: collapse;
    margin-bottom: 20px;
  }
  
  .invoice-table th, .invoice-table td {
    border: 1px solid #ccc;
    padding: 8px;
    text-align: left;
  }
  
  .notes, .total, .footer {
    margin-top: 20px;
  }
  
  .total p {
    font-size: 1.2em;
    font-weight: bold;
  }
  
  .footer p {
    font-size: 0.8em;
    color: #888;
  }
  </style>
  