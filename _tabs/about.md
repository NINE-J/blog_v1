---
# the default layout is 'page'
icon: fas fa-info-circle
order: 4
---

<style>
  #reset-button-wrap {
    display: flex;
    align-items: center;
    justify-content: center;
  }
  
  #reset-button {
    width: 48px;
    height: 48px;
    border-radius: 24px;
    border: none;
    cursor: pointer;
    background-color: #007bff;
  }

  .ico-reload {
    width: 80%;
    height: 80%;
    fill: #fff;
  }

  .rotate {
    transition: transform 1s ease-in-out;
  }

  .rotate.active {
    transform: rotate(360deg);
  }
</style>

<div id="random-quote" class="prompt-tip"></div>
<div id="reset-button-wrap">
  <button id="reset-button">
    <svg class="ico-reload rotate" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><!--!Font Awesome Free 6.7.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2025 Fonticons, Inc.--><path d="M463.5 224l8.5 0c13.3 0 24-10.7 24-24l0-128c0-9.7-5.8-18.5-14.8-22.2s-19.3-1.7-26.2 5.2L413.4 96.6c-87.6-86.5-228.7-86.2-315.8 1c-87.5 87.5-87.5 229.3 0 316.8s229.3 87.5 316.8 0c12.5-12.5 12.5-32.8 0-45.3s-32.8-12.5-45.3 0c-62.5 62.5-163.8 62.5-226.3 0s-62.5-163.8 0-226.3c62.2-62.2 162.7-62.5 225.3-1L327 183c-6.9 6.9-8.9 17.2-5.2 26.2s12.5 14.8 22.2 14.8l119.5 0z"/></svg>
  </button>
</div>

<script>
  const quoteElement = document.getElementById('random-quote');
  const resetButton = document.getElementById('reset-button');

  function displayRandomQuote() {
    const reloadIcon = document.querySelector('.ico-reload');
    reloadIcon.classList.toggle('active');

    fetch('https://api.quotable.io/quotes/random')
      .then(response => response.json())
      .then(data => {
        const quote = data.content;
        const author = data.author;
        quoteElement.innerHTML = `<blockquote class="prompt-tip">${quote}<br>— ${author}</blockquote>`;
      })
      .catch(error => {
        console.error('API 호출 오류:', error);
        quoteElement.innerHTML = '<blockquote class="prompt-tip">감자에 싹이 나서 잎이 나면 묵찌바가 가능하다.<br>— Nine</blockquote>';
      });
  }

  displayRandomQuote();

  resetButton.addEventListener('click', displayRandomQuote);
</script>
