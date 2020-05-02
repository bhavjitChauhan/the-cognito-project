<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <a class="navbar-brand" href="#">Cognito</a>
      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarNav"
        aria-controls="navbarNav"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
          <li class="nav-item">
            <a class="nav-link" data-toggle="modal" data-target="#aboutModal">About</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" data-toggle="modal" data-target="#usageModal">Usage</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" data-toggle="modal" data-target="#contactModal">Contact</a>
          </li>
        </ul>
      </div>
    </nav>
    <div class="modal fade" id="aboutModal" tabindex="-1" role="dialog" aria-hidden="true">
      <div class="modal-dialog modal-l" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLongTitle">About</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <p>A search engine that queries results from academic databases. The project was built with accessible future expansion in mind.</p>
            <h6>Why?</h6>
            <p>o Google is a great option for general use, but it isn’t the best for seeking academic resources, Google Scholar is a product that tries to address these issues and offers a vast number of articles but does not return results that may be helpful for looking at a topic at a glance, like ones from Wikipedia.</p>
            <h6>Technical Information</h6>
            <p>Built with</p>
            <ul>
              <li>Vue.js</li>
              <li>Bootstrap</li>
              <li>Gulp</li>
            </ul>
            <p>
              You can view all of the dependencies using the
              <a
                href="https://github.com/bhavjitChauhan/the-cognito-project/network/dependencies"
                target="_blank"
              >Dependency graph</a> at the
              <a
                href="https://github.com/bhavjitChauhan/the-cognito-project"
                target="_blank"
              >project repository</a>
            </p>
          </div>
        </div>
      </div>
    </div>
    <div class="modal fade" id="usageModal" tabindex="-1" role="dialog" aria-hidden="true">
      <div class="modal-dialog modal-l" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLongTitle">Usage</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <p>To use the search engine, follow these steps</p>
            <ol>
              <li>
                Enter your query in the search box and press the
                <kbd>Enter</kbd> key or the
                <font-awesome-icon icon="search" />button
              </li>
              <li>View the results</li>
              <li>Click one of the buttons or links to visit the resource</li>
            </ol>
          </div>
        </div>
      </div>
    </div>
    <div class="modal fade" id="contactModal" tabindex="-1" role="dialog" aria-hidden="true">
      <div class="modal-dialog modal-l" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLongTitle">Contact</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <p>
              Please report any issues or questions at the
              <a
                href="https://github.com/bhavjitChauhan/the-cognito-project"
                target="_blank"
              >project repository</a>.
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Navbar"
};
</script>

<style scoped>
</style>
