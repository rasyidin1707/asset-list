<template>
  <div class="home">
    <h1>Asset List</h1>
    <table border="1" cellpadding="5" cellspacing="0">
      <thead>
        <tr>
          <th>Asset Name</th>
          <th>Department</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(asset, index) in assets" :key="index">
          <td>{{ asset.name }}</td>
          <td>{{ asset.department }}</td>
        </tr>
      </tbody>
    </table>
    <br />
    <button @click="downloadCSV">Download CSV</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      assets: [
        { name: "Printer", department: "HR" },
        { name: "Monitor", department: "IT" },
        { name: "Barcode Scanner", department: "ACCOUNT" },
      ],
    };
  },
  methods: {
    downloadCSV() {
      const csvContent = "data:text/csv;charset=utf-8,"
        + this.assets.map(asset => `${asset.name},${asset.department}`).join("\n");
      
      const encodedUri = encodeURI(csvContent);
      const link = document.createElement("a");
      link.setAttribute("href", encodedUri);
      link.setAttribute("download", "assets.csv");
      document.body.appendChild(link);
      link.click();
    },
  },
};
</script>

<style scoped>
table {
  width: 50%;
  margin: auto;
  border-collapse: collapse;
}

th, td {
  padding: 8px 12px;
  text-align: left;
}
</style>
