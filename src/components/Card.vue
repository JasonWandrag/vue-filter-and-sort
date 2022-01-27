<template>
  <div class="card">
    <div class="container">
      <img :src="img" alt="cookies" class="hero-image" />

      <div class="information">
        <img
          :src="person.picture.large"
          :alt="person.name.first"
          class="avatar"
        />
        <div class="name">{{ person.name.first }} {{ person.name.last }}</div>
        <div class="position">{{ person.gender }}</div>

        <div class="stats">
          <span class="followers">
            <span class="value">{{ person.dob.age }}</span>
            <span class="label">age</span>
          </span>

          <span class="following">
            <span class="value">{{ person.location.country }}</span>
            <span class="label">country</span>
          </span>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: ["person", "idx"],
  mounted() {
    console.log(this.person);
  },
  data() {
    return {
      img: "https://picsum.photos/300/?random=" + this.idx,
    };
  },
};
</script>
<style>
.card {
  font: 13px/23px "Raleway", Arial, sans-serif;
  color: #303336;
  overflow: hidden;
  margin: 20px;
  background: rgba(255, 255, 255, 0.4);
  box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
  backdrop-filter: blur(4px);
  -webkit-backdrop-filter: blur(4px);
  border-radius: 10px;
}

.container {
  margin: 0 auto;
  width: 300px;
  height: 465px;
  border-radius: 3px;
  position: relative;
}

.hero-image {
  width: 100%;
  height: 50%;
  object-fit: cover;
}

.information {
  text-align: center;
  background: none;
}

.avatar {
  margin: 0 auto;
  margin: -82px auto 15px;
  display: block;
}

.name {
  font-size: 22px;
}

.position {
  font-size: 16px;
  color: #8c98a8;
  margin-bottom: 24px;
}

.stats {
  margin: auto;
  border-top: 1px solid #ced5e0;
  width: 240px;
}
.stats .followers,
.stats .following,
.stats .stories {
  display: inline-block;
  padding: 6px 10px 0;
}
.stats .followers {
  border-right: 1px solid #ced5e0;
}
.stats .value {
  font-size: 18px;
  font-weight: 600;
}
.stats .label {
  display: block;
  font-size: 14px;
  color: #8c98a8;
}
</style>
