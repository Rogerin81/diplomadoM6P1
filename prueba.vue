<form @submit.prevent="save()">
    <table class="table table-striped">
        <thead>
        <tr>
            <th colspan="2">

                <select class="form-select" aria-label="Default select example" v-model="newLink.type">
                    <option v-for="type in types" :value="type" :key="type">{{type}}</option>
                </select>

            </th>
            <th>

                <input type="text" class="form-control" id="description" v-model="newLink.description">

            </th>
            <th>
                <input type="url" class="form-control" id="link" v-model="newLink.url">
            </th>
            <th>
                <button type="submit" class="btn btn-primary">Agregar</button>
            </th>
        </tr>
        <tr>
            <th scope="col">Id</th>
            <th scope="col">Nombre</th>
            <th scope="col">Email</th>
            <th scope="col">Dirección</th>
            <th scope="col">Teléfono</th>
            <th scope="col">Pais</th>
            <th scope="col">Ciudad</th>
            <th scope="col">Acciones</th>
        </tr>
        </thead>

        <tbody>
        <tr v-for="(link, index) in getList()" :key="index">
            <th scope="row">{{ contact.id }}</th>
            <td>{{ contact.name }}</td>
            <td>{{ contact.email }}</td>
            <td>{{ contact.address }}</td>
            <td>{{ contact.phone }}</td>
            <td>{{ contact.country }}</td>
            <td>{{ contact.city }}</td>
            <td>
                
            </td>
        </tr>
        </tbody>
    </table>
</form>
</div>
</div>

<!-- Modal -->
<div class="modal fade" id="editModal" tabindex="-1" aria-labelledby="editModalLabel" aria-hidden="true">
<div class="modal-dialog">
<div class="modal-content">
    <div class="modal-header">
        <h1 class="modal-title fs-5" id="editModalLabel">Editar</h1>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
    </div>
    <form @submit.prevent="saveEdit()">
        <div class="modal-body" v-if="itemSelected">


            <div class="mb-3">
                <label for="updateType" class="form-label">Tipo de link</label>
                <select class="form-select" v-model="itemSelected.type" id="updateType">
                    <option v-for="type in types" :value="type">{{type}}</option>
                </select>
            </div>
            <div class="mb-3">
                <label for="updateDescription" class="form-label">Descripción</label>
                <input type="text" v-model="itemSelected.description" class="form-control"
                       id="updateDescription">
            </div>
            <div class="mb-3">
                <label for="updateUrl" class="form-label">URL</label>
                <input type="text" v-model="itemSelected.url" class="form-control" id="updateUrl">
            </div>

        </div>
        <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cancelar</button>
            <button type="submit" class="btn btn-primary">Guardar cambios</button>
        </div>
    </form>
</div>