<script>
  import { onMount } from "svelte";
  import Header from "../components/Header.svelte";
  import Sidebar from "../components/Sidebar.svelte";
  import Timeline from "../components/Timeline.svelte";
  import Main from "../components/Main.svelte";

  let users = [];
  let catsPhotos = [];
  const API_CATS = "https://api.thecatapi.com/v1/images/search?limit=10";
  const API_USERS = "https://randomuser.me/api/?results=10";

  onMount(async () => {
    const descriptionPhrases = {
      0: "My beloved cat",
      1: "The pet that I always wanted",
      2: "New cat",
      3: "Just Chilling",
      4: "❤️❤️❤️",
      5: "🐱❤️",
      6: "Samuel is the perfect name for this cat",
      7: "I love it",
      8: "Meow",
      9: "🐈"
    };
    const responseUsers = await fetch(API_USERS);
    const responseCats = await fetch(API_CATS);
    let usersResult = await responseUsers.json();
    let usersArray = usersResult.results;
    catsPhotos = await responseCats.json();
    users = usersArray.map((user, index) => {
      user.cat = catsPhotos[index];
      user.phrase = descriptionPhrases[index];
      return user;
    });
  });
</script>

<style>
  @import url("https://fonts.googleapis.com/css?family=Lato:300,400&display=swap");
  @import url("https://fonts.googleapis.com/css?family=Pacifico&display=swap");
  :global(body) {
    background-color: #fafafa;
    color: rgba(38, 38, 38, 0.7);
    font-family: "Lato", sans-serif;
    margin: 0;
    padding: 0;
  }
  :global(h1, h2, h3) {
    margin: 0;
    padding: 0;
  }
</style>

<Header />
<Main>
  <Timeline posts={users} />
  <Sidebar />
</Main>
