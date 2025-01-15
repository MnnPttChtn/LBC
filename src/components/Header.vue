<script setup></script>
<template>
  <header>
    <div class="container">
      <div class="top">
        <RouterLink to="/">
          <img src="../assets/img/logo.svg" alt="logo" />
        </RouterLink>

        <div class="middle">
          <button>
            <font-awesome-icon :icon="['far', 'plus-square']" />
            <span>Déposer une annonce</span>
          </button>
          <div class="search">
            <input type="text" name="search" id="search" placeholder="Rechercher sur leboncoin" />
            <font-awesome-icon :icon="['fas', 'magnifying-glass']" />
          </div>
        </div>

        <div class="right">
          <font-awesome-icon :icon="['far', 'user']" />
          <p>Se connecter</p>
        </div>
      </div>

      <div class="bottom">
        <span>Immobilier</span>
        <font-awesome-icon :icon="['fas', 'circle']" />
        <span>Véhicules</span>
        <font-awesome-icon :icon="['fas', 'circle']" />
        <span>Locations de vacances</span>
        <font-awesome-icon :icon="['fas', 'circle']" />
        <span>Emploi</span>
        <font-awesome-icon :icon="['fas', 'circle']" />
        <span>Mode</span>
        <font-awesome-icon :icon="['fas', 'circle']" />
        <span> Maison & Jardin</span>
        <font-awesome-icon :icon="['fas', 'circle']" />
        <span> Famille</span>
        <font-awesome-icon :icon="['fas', 'circle']" />
        <span> Electronique</span>
        <font-awesome-icon :icon="['fas', 'circle']" />
        <span> Loisirs</span>
        <font-awesome-icon :icon="['fas', 'circle']" />
        <span> Autres</span>
      </div>
    </div>
  </header>
</template>

<style scoped>
header {
  border-bottom: 1px solid var(--grey);
  height: var(--header-height);
}
.container {
  padding: 10px 0 20px 0;
  display: flex;
  flex-direction: column;
  gap: 30px;
}

/* TOP*/

img {
  width: 140px;
}

.top {
  display: flex;
  justify-content: space-between;
}

.top p {
  font-size: 12px;
}

.middle {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 20px;
}

.search {
  display: flex;
  background-color: var(--grey-light);
  padding: 7px;
  border-radius: 10px;
  width: 300px;
}

.search input {
  background-color: inherit;
  border: none;
  flex: 1;
}
.search svg {
  background-color: var(--orange);
  padding: 8px;
  box-sizing: content-box;
  border-radius: 7px;
}

.search input::placeholder {
  color: var(--black);
  font-size: 16px;
}

.middle button {
  background-color: var(--orange);
  color: white;
  padding: 10px;
  border: none;
  border-radius: 10px;

  font-weight: bold;
}

.middle span {
  margin-left: 10px;
}

.right {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
}

/* BOTTOM*/

.bottom {
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 14px;
}

.bottom svg {
  color: var(--black);
  font-size: 2px;
}
</style>
