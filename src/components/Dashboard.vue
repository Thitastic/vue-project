<template>
  <div ref="wrapper" class="page-wrapper chiller-theme toggled">
    <nav id="sidebar" class="sidebar-wrapper">
      <div class="sidebar-content">
        <div class="sidebar-brand">
          <a href="#">HOME</a>
        </div>
        <div class="sidebar-header">
          <div class="user-pic">
            <img
              class="img-responsive img-rounded"
              src="https://raw.githubusercontent.com/azouaoui-med/pro-sidebar-template/gh-pages/src/img/user.jpg"
              alt="User picture"
            />
          </div>
          <div class="user-info">
            <span class="user-name">Hello Admin</span>
            <span class="user-role">Administrator</span>
            <span class="user-status">
              <i class="fa fa-circle"></i>
              <span>Online</span>
            </span>
          </div>
        </div>
        <!--Admin action-->
        <div class="sidebar-admin">
          <a href="#" title="Notifications">
            <i class="fa fa-bell"></i>
          </a>
          <a href="#" title="Message">
            <i class="fa fa-envelope"></i>
          </a>
          <a href="#" title="Settings">
            <i class="fa fa-cog"></i>
          </a>
          <a href="#" title="Sign out">
            <i class="fa fa-power-off"></i>
          </a>
        </div>
        <!-- sidebar-search  -->
        <div class="sidebar-menu">
          <ul>
            <li class="sidebar-item">
              <a href="#">
                <i class="fas fa-columns"></i>
                <span>Dashboard</span>
              </a>
            </li>
            <li class="sidebar-item">
              <a href="#">
                <i class="fas fa-user"></i>
                <span>Authorization</span>
              </a>
            </li>
          </ul>
        </div>
        <!-- sidebar-menu  -->
      </div>
      <!-- sidebar-content  -->
    </nav>
    <!-- sidebar-wrapper  -->
    <main class="page-content">
      <div class="container-fluid">
        <!--Sticky bar action-->
        <div class="sticky-bar">
          <button @click="expandMenu()" id="show-bar" class="btn btn-primary">
            <i class="fas fa-bars"></i> Menu
          </button>
          <button
            type="button"
            class="btn btn-primary"
            data-toggle="modal"
            data-target="#addProductModal"
          >
            <i class="fas fa-plus"></i> New
          </button>
          <button
            type="button"
            class="btn btn-primary"
            data-toggle="modal"
            data-target="#filterModal"
          >
            <i class="fas fa-filter"></i> Filter
          </button>
          <input
            v-model="key"
            class="form-control"
            type="text"
            name="key"
            id="searchKey"
            placeholder="Search..."
          />
          <button type="buttom" @click="search(key)" class="btn btn-primary">
            Search
          </button>
          <div class="alert alert-primary" role="alert">{{ alertMessage }}</div>
        </div>

        <!--Tables-->
        <table class="table table-hover">
          <thead>
            <tr class="bg-primary">
              <th class="col-sm">ID</th>
              <th class="col-md">Image</th>
              <th @click="sortByName()" class="col-md">Name</th>
              <th @click="sortByPrice()" class="col-md">Price</th>
              <th class="col-sm">Category</th>
              <th class="col-sm">Brand</th>
              <th class="col-lg">Actions</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="key in cloneListProduct" :key="key.id">
              <th scope="row">{{ key.id }}</th>
              <td>
                <div class="item-img">
                  {{ key.image }}
                </div>
              </td>
              <td>{{ key.name }}</td>
              <td>{{ key.price }}</td>
              <td>{{ key.category }}</td>
              <td>{{ key.brand }}</td>
              <td>
                <button
                  v-bind:id="key.id"
                  @click="getId(key.id)"
                  type="button"
                  data-toggle="modal"
                  data-target="#confirmDeleteModal"
                  class="btn btn-danger"
                >
                  <i class="fas fa-times"></i>
                </button>
                <button
                  v-bind:id="key.id"
                  @click="getData(key.id)"
                  type="button"
                  class="btn btn-primary"
                  data-toggle="modal"
                  data-target="#editProductModal"
                >
                  <i class="fas fa-pencil-alt"></i>
                </button>
                <button class="btn btn-primary">
                  <i class="fas fa-eye"></i>
                </button>
              </td>
            </tr>
          </tbody>
        </table>
        <!--New Modal-->
        <!-- Modal NEW -->
        <div
          class="modal fade"
          id="addProductModal"
          tabindex="-1"
          role="dialog"
          aria-labelledby="myLargeModalLabel"
          aria-hidden="true"
        >
          <div class="modal-dialog modal-lg" role="document">
            <div class="modal-content">
              <div class="modal-header bg-primary">
                <h5 class="modal-title" id="exampleModalLabel">New...</h5>
              </div>
              <div class="modal-body">
                <label for="productName">Product name:</label>
                <input
                  v-model="productName"
                  class="form-control"
                  type="text"
                  name="productName"
                  id="productName"
                />
                <label for="productPrice">Price:</label>
                <input
                  v-model="productPrice"
                  class="form-control"
                  type="number"
                  name="productPrice"
                  id="productPrice"
                />
                <label for="productBrand">Brand/ Factory</label>
                <select
                  v-model="productBrand"
                  class="custom-select"
                  data-live-search="true"
                >
                  <option v-bind:value="1" data-token="Casio">Casio</option>
                  <option v-bind:value="2" data-token="Rolex">Rolex</option>
                </select>
                <label for="productCategory">Category</label>
                <select
                  v-model="productCategory"
                  class="custom-select"
                  data-live-search="true"
                >
                  <option v-bind:value="1" data-token="G-shock">G-shock</option>
                  <option v-bind:value="2" data-token="Air-king">
                    Air-king
                  </option>
                </select>
                <label for="fileUpload">Image</label>
                <div class="input-group">
                  <div class="input-group-prepend">
                    <span class="input-group-text" id="inputGroupFileAddon01"
                      >Upload</span
                    >
                  </div>
                  <div class="custom-file">
                    <input
                      type="file"
                      class="custom-file-input"
                      id="inputGroupFile01"
                      aria-describedby="inputGroupFileAddon01"
                    />
                    <label class="custom-file-label" for="inputGroupFile01"
                      >Choose file</label
                    >
                  </div>
                </div>
              </div>
              <div class="modal-footer">
                <button
                  type="button"
                  class="btn btn-danger"
                  data-dismiss="modal"
                >
                  Cancel
                </button>
                <button
                  @click="
                    addProduct(
                      productName,
                      productPrice,
                      productBrand,
                      productCategory
                    )
                  "
                  type="button"
                  class="btn btn-primary"
                  data-dismiss="modal"
                >
                  Save
                </button>
              </div>
            </div>
          </div>
        </div>
        <!--Modal edit-->
        <div
          class="modal fade"
          id="editProductModal"
          tabindex="-1"
          role="dialog"
          aria-labelledby="myLargeModalLabel"
          aria-hidden="true"
        >
          <div class="modal-dialog modal-lg" role="document">
            <div class="modal-content">
              <div class="modal-header bg-primary">
                <h5 class="modal-title" id="editProductModalHeader">Edit</h5>
              </div>
              <div class="modal-body">
                <label for="productName">Product name:</label>
                <input
                  v-model="productName"
                  class="form-control"
                  type="text"
                  name="productName"
                  id="productName"
                />
                <label for="productPrice">Price:</label>
                <input
                  v-model="productPrice"
                  class="form-control"
                  type="number"
                  name="productPrice"
                  id="productPrice"
                />
                <label for="productBrand">Brand/ Factory</label>
                <select
                  v-model="productBrand"
                  class="custom-select"
                  data-live-search="true"
                >
                  <option selected>Choose---</option>
                  <option
                    v-if="productBrand === 1"
                    selected
                    v-bind:value="1"
                    data-token="Casio"
                  >
                    Casio
                  </option>
                  <option v-else value="1" data-token="Casio">Casio</option>
                  <option
                    v-if="productBrand === 2"
                    selected
                    v-bind:value="2"
                    data-token="Rolex"
                  >
                    Rolex
                  </option>
                  <option v-else value="2" data-token="Rolex">Rolex</option>
                </select>
                <label for="productCategory">Category</label>
                <select
                  v-model="productCategory"
                  class="custom-select"
                  data-live-search="true"
                >
                  <option selected>Choose---</option>
                  <option
                    v-if="productCategory === 1"
                    selected
                    v-bind:value="1"
                    data-token="G-shock"
                  >
                    G-shock
                  </option>
                  <option v-else selected v-bind:value="1" data-token="G-shock">
                    G-shock
                  </option>
                  <option
                    v-if="productCategory === 2"
                    selected
                    v-bind:value="2"
                    data-token="Air-king"
                  >
                    Air-king
                  </option>
                  <option v-else v-bind:value="2" data-token="Air-king">
                    Air-king
                  </option>
                </select>
                <label for="fileUpload">Image</label>
                <div class="input-group">
                  <div class="input-group-prepend">
                    <span class="input-group-text" id="fileEdit">Upload</span>
                  </div>
                  <div class="custom-file">
                    <input
                      type="file"
                      class="custom-file-input"
                      id="fileEdit_"
                      aria-describedby="inputGroupFileAddon01"
                    />
                    <label class="custom-file-label" for="inputGroupFile01"
                      >Choose file</label
                    >
                  </div>
                </div>
              </div>
              <div class="modal-footer">
                <button
                  type="button"
                  class="btn btn-danger"
                  data-dismiss="modal"
                >
                  Cancel
                </button>
                <button
                  @click="
                    edit(
                      productId,
                      productName,
                      productCategory,
                      productBrand,
                      productPrice
                    )
                  "
                  type="button"
                  class="btn btn-primary"
                  data-dismiss="modal"
                >
                  Save
                </button>
              </div>
            </div>
          </div>
        </div>
        <!--Modal confirm delete-->
        <div
          class="modal fade"
          id="confirmDeleteModal"
          tabindex="-1"
          role="dialog"
          aria-labelledby="exampleModalLabel"
          aria-hidden="true"
        >
          <div class="modal-dialog" role="document">
            <div class="modal-content">
              <div class="modal-header bg-danger text-white">
                <h5 class="modal-title" id="confirmDelete">Confirm Delete</h5>
              </div>
              <div class="modal-body">Delete 1 row?</div>
              <div class="modal-footer">
                <button
                  @click="remove()"
                  type="button"
                  class="btn btn-danger"
                  data-dismiss="modal"
                >
                  Delete
                </button>
                <button
                  type="button"
                  class="btn btn-secondary"
                  data-dismiss="modal"
                >
                  Cancel
                </button>
              </div>
            </div>
          </div>
        </div>
        <!--Modal filter-->
        <div
          class="modal fade"
          id="filterModal"
          tabindex="-1"
          role="dialog"
          aria-labelledby="exampleModalLabel"
          aria-hidden="true"
        >
          <div class="modal-dialog" role="document">
            <div class="modal-content">
              <div class="modal-header bg-warning text-white">
                <h5 class="modal-title" id="filter-title">Filter...</h5>
              </div>
              <div class="modal-body">
                <h5>Category</h5>
                <input
                  v-model="filterGshock"
                  class="checkbox"
                  type="checkbox"
                  name="checkboxCategory"
                  id="chkGshock"
                />
                <label for="gshock">G-Shock</label>
                <input
                  v-model="filterAirking"
                  class="checkbox"
                  type="checkbox"
                  name="checkboxCategory"
                  id="chkAirking"
                />
                <label for="gshock">Air King</label>
                <h5>Price</h5>
                <!--Price-->
                <div class="form-check">
                  <input
                    v-model="filterPrice"
                    class="form-check-input"
                    type="radio"
                    name="priceLow"
                    id="rdoPriceLow"
                    value="priceLow"
                  />
                  <label class="form-check-label" for="exampleRadios2">
                    &lt; 1,000,000
                  </label>
                </div>
                <div class="form-check">
                  <input
                    v-model="filterPrice"
                    class="form-check-input"
                    type="radio"
                    name="priceLow"
                    id="rdoPriceMedium"
                    value="priceMed"
                  />
                  <label class="form-check-label" for="exampleRadios2">
                    1,000,000 - 5,000,000
                  </label>
                </div>
                <div class="form-check">
                  <input
                    v-model="filterPrice"
                    class="form-check-input"
                    type="radio"
                    name="priceLow"
                    id="rdoPriceHigh"
                    value="priceHig"
                  />
                  <label class="form-check-label" for="exampleRadios2">
                    &gt; 5,000,000
                  </label>
                </div>
              </div>
              <div class="modal-footer">
                <button type="button" class="btn btn-primary">Clear</button>
                <button
                  @click="filter()"
                  type="button"
                  class="btn btn-primary"
                  data-dismiss="modal"
                >
                  Apply
                </button>
                <button
                  type="button"
                  class="btn btn-secondary"
                  data-dismiss="modal"
                >
                  Cancel
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </main>
    <!--Toast-->

    <!-- page-content" -->
  </div>
</template>

<script>
export default {
  name: "Dashboard",
  data() {
    return {
      toggleIsOpen: true,
      alertMessage: "",
      maxId: 2,
      productId: null,
      productName: "",
      productPrice: "",
      productImage: "",
      productBrand: "",
      productCategory: "",
      nameReverse: false,
      priceReverse: false, 


      key: "",


      filterGshock: false,
      filterAirking: false,
      filterPrice: "",
      listProduct: [
        {
          id: 1,
          name: "Casio G-SHOCK GA-100-1A1DR Nam Quartz",
          price: 2426000,
          category: "G-shock",
          brand: "CASIO",
          image: "g-shock-ga-700-1bdr.jpg",
        },
        {
          id: 2,
          name: "ROLEX AIR-KING 116900-0001 WATCH 40",
          price: 163618000,
          category: "Air King",
          brand: "Rolex",
          image: "rolex-116900-air-king-watch-40mm1.png",
        },
      ],
      cloneListProduct: [
        {
          id: 1,
          name: "Casio G-SHOCK GA-100-1A1DR Nam Quartz",
          price: 2426000,
          category: "G-shock",
          brand: "CASIO",
          image: "g-shock-ga-700-1bdr.jpg",
        },
        {
          id: 2,
          name: "ROLEX AIR-KING 116900-0001 WATCH 40",
          price: 163618000,
          category: "Air King",
          brand: "Rolex",
          image: "rolex-116900-air-king-watch-40mm1.png",
        },
      ],
    };
  },
  methods: {
    expandMenu: function () {
      const _wrap = this.$refs["wrapper"];
      if (this.toggleIsOpen === true) {
        _wrap.classList.remove("toggled");
        this.toggleIsOpen = false;
      } else {
        _wrap.classList.add("toggled");
        this.toggleIsOpen = true;
      }
    },
    //Method thêm sp
    addProduct: function (pName, pPrice, pBrand, pCategory) {
      this.maxId++;
      let _brand = "";
      let _category = "";
      if (pBrand === 1) {
        _brand = "CASIO";
      } else _brand = "Rolex";
      if (pCategory === 1) {
        _category = "G-Shock";
      } else _category = "Air King";

      let product = {
        id: this.maxId,
        name: pName,
        price: pPrice,
        category: _category,
        brand: _brand,
        image: "Imageurl",
      };
      this.listProduct.push(product);
      this.cloneListProduct = this.listProduct;
      this.alertMessage = "1 row added.";

      //Remove values 
      this.productName = '';
      this.productPrice = null;
      this.productBrand = null;
      this.productCategory = null;
    },
    getData: function (pId) {
      this.productId = pId;
      this.listProduct.forEach((element, index) => {
        if (element.id === pId) {
          this.productName = element.name;
          if (element.brand === "CASIO") {
            this.productBrand = 1;
          } else {
            this.productBrand = 2;
          }
          this.productPrice = element.price;
          if (element.category === "G-Shock") {
            this.productCategory = 1;
          } else {
            this.productCategory = 2;
          }
          return;
        }
      });
    },
    edit: function (pId, pName, pCategory, pBrand, pPrice) {
      this.listProduct.forEach((element) => {
        if (element.id === pId) {
          element.name = pName;
          element.price = pPrice;
          element.category = pCategory;
          if (pBrand === 1) {
            element.brand = "CASIO";
          } else {
            element.brand = "Rolex";
          }
          if (pCategory === 1) {
            element.category = "G-Shock";
          } else {
            element.category = "Air King";
          }
          //copy array
          this.cloneListProduct = this.listProduct;
          return;
        }
      });
    },
    remove: function () {
      this.listProduct.forEach((element, index, object) => {
        if (element.id === this.productId) {
          object.splice(index, 1);
          this.cloneListProduct = this.listProduct;
          this.productId = null;
          return;
        }
      });
    },
    getId: function (pId) {
      this.productId = pId;
    },
    sortByName: function () {
      if (this.nameReverse === true) {
        this.nameReverse = false;
        this.cloneListProduct.sort(function (a, b) {
          if (a.name < b.name) {
            return 1;
          }
          if (a.name > b.name) {
            return -1;
          }
          return 0;
        });
      } else {
        this.nameReverse = true;
        this.cloneListProduct.sort(function (a, b) {
          if (a.name < b.name) {
            return -1;
          }
          if (a.name > b.name) {
            return 1;
          }
          return 0;
        });
      }
    },
    sortByPrice: function () {
      if (this.nameReverse === true) {
        this.nameReverse = false;
        this.cloneListProduct.sort(function (a, b) {
          if (a.price < b.price) {
            return 1;
          }
          if (a.price > b.price) {
            return -1;
          }
          return 0;
        });
      } else {
        this.nameReverse = true;
        this.cloneListProduct.sort(function (a, b) {
          if (a.price < b.price) {
            return -1;
          }
          if (a.price > b.price) {
            return 1;
          }
          return 0;
        });
      }
    },
    search: function (key) {
      let regex = new RegExp( key, 'gi' );
      if (key === "") {
        this.cloneListProduct = this.listProduct;
      } else {
        let searchArr = [];
        this.listProduct.forEach((element) => {
          if (element.name.match(regex)) {
            searchArr.push(element);
          }
        });
        this.cloneListProduct = searchArr;
      }
    },
    //Phuong thuc loc san pham
    filter: function () {
      //Neu mot trong hai checkbox duoc chon
      if (this.filterGshock || this.filterAirking) {
        //Mảng ảo
        let temp = [];
        //Nếu check vào ô G shock 
        if (this.filterGshock === true) {
          //Duyệt mảng, tìm đối tượng có chưa category g shock
          this.cloneListProduct.forEach((element) => {
            //Nếu tìm thấy thêm đối tượng vào mảng temp
            if (element.category === "G-shock") {
              temp.push(element);
            }
          });
        //Nếu không làm ngược lại
        } else {
          this.cloneListProduct.forEach((element) => {
            if (element.category === "Air King") {
              temp.push(element);
            }
          });
        }
        this.cloneListProduct = temp;
      }
    },
  },
};
</script>

<style>
@import url("../assets/style/dashboard.css");
</style>