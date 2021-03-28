<template>
  <main>
    <section class="section is-full-height">
      <div class="bg"></div>
      <div class="container">
        <div class="row align-items-center mb-negative--large">
          <div class="col-12 col-md-7 col-lg-7 mb--large">
            <div class="col-inner">
              <h1>About me</h1>
              <p class="lead-text">Something about me:</p>
              <p>
                Lorem ipsum dolor sit amet consectetur adipisicing elit. Vel
                qui, voluptatum deserunt similique modi fugit laudantium?
                Nostrum alias eligendi laborum blanditiis praesentium enim illum
                optio quidem possimus eius soluta, quis reprehenderit debitis
                consequatur sed tempora iusto, similique ea perferendis culpa
                saepe. Reprehenderit et, quaerat eaque asperiores vel a
                repellendus esse?
              </p>
            </div>
          </div>
          <div class="col-12 col-md-5 col-lg-4 offset-lg-1 mb--large">
            <div class="col-inner">
              <TodoList />
            </div>
          </div>
        </div>
      </div>
    </section>
  </main>
</template>

<script>
import TodoList from "@/components/TodoList.vue";
export default {
  name: "About",
  components: {
    TodoList,
  },
};
</script>