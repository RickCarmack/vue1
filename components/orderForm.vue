<template>
  <form id="order">
    <div class="head">Rally: <input type="text" name="rally"> Date: <input type="text" name="date"> Staff: <input type="text" name="staff"></div>
    <br>
    <div class="table-responsive">
    <table class="table table-bordered">
      <thead>
        <tr><th></th><th>Sphere</th><th>Cylinder</th><th>Axis</th><th>Prism</th><th>Add Power</th><th>PD</th></tr>
      </thead>
      <tbody>
        <tr><td>R</td><td></td><td></td><td></td><td></td><td></td><td></td></tr>
        <tr><td>L</td><td></td><td></td><td></td><td></td><td></td><td></td></tr>
        <tr>
          <td colspan="2"><input type="checkbox" name="holdrx"> Hold for Rx</td>
          <td colspan="2"><input type="checkbox" name="getrx"> Get Rx (signed release)</td>
          <td colspan="2"><input type="checkbox" name="offlens"> Off Lensometer by: <input type="text" name="lensStaff"></td>
          <td><input type="checkbox" name="writrx"> Written Rx</td>
        </tr>
        <tr>
          <td colspan="2">Lens Style <input type="text" name="lensStyle"></td>
          <td colspan="4">Materials <input type="text" name="materials"></td>
        </tr>
      </tbody>
    </table>
    </div>
  </form>
</template>
<script>
  export default {}
</script>
<style>
.head {
  text-align: center;
}
</style>
