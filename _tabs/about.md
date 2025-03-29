---
# the default layout is 'page'
icon: fas fa-info-circle
order: 4
---

<style>
  #random-quote .quote-profile {
    font-size: 12px;
    opacity: 0.6;
  }

  #reload-button-wrap {
    display: flex;
    align-items: center;
    justify-content: center;
  }
  
  #reload-button-wrap #reload-button {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 48px;
    height: 48px;
    border-radius: 24px;
    border: none;
    cursor: pointer;
    background-color: #F90909;
    opacity: 0.4;
  }

  #reload-button-wrap #reload-button:hover {
    opacity: 1;
  }

  #reload-button-wrap .ico-reload {
    width: 80%;
    height: 80%;
    fill: #fff;
  }

  #reload-button-wrap .rotate {
    transition: transform 1s ease-in-out;
  }

  #reload-button-wrap .rotate.active {
    transform: rotate(360deg);
  }
</style>

<div id="random-quote" class="prompt-tip"></div>
<div id="reload-button-wrap">
  <button id="reload-button">
    <svg class="ico-reload rotate" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><!--!Font Awesome Free 6.7.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2025 Fonticons, Inc.--><path d="M463.5 224l8.5 0c13.3 0 24-10.7 24-24l0-128c0-9.7-5.8-18.5-14.8-22.2s-19.3-1.7-26.2 5.2L413.4 96.6c-87.6-86.5-228.7-86.2-315.8 1c-87.5 87.5-87.5 229.3 0 316.8s229.3 87.5 316.8 0c12.5-12.5 12.5-32.8 0-45.3s-32.8-12.5-45.3 0c-62.5 62.5-163.8 62.5-226.3 0s-62.5-163.8 0-226.3c62.2-62.2 162.7-62.5 225.3-1L327 183c-6.9 6.9-8.9 17.2-5.2 26.2s12.5 14.8 22.2 14.8l119.5 0z"/></svg>
  </button>
</div>

<script>
  const quoteElement = document.getElementById('random-quote');
  const reloadButton = document.getElementById('reload-button');

  function displayRandomQuote() {
    const reloadIcon = document.querySelector('.ico-reload');
    reloadIcon.classList.toggle('active');

    fetch('https://korean-quotes-api.vercel.app/api', {
      method: "GET",
      headers: {
        "Content-Type": "application/json",
      },
      credentials: "omit", // 명시적으로 설정 (기본값이지만 확실히 하기 위함)
      cache: "no-store", // 캐시 방지
    })
      .then(response => {
        if (!response.ok) {
          throw new Error(`HTTP error! status: ${response.status}`);
        }
        return response.json();
      })
      .then(data => {
        const author = data.author;
        const profile = data.profile;
        const content = data.content;
        quoteElement.innerHTML = `<blockquote class="prompt-tip">"${content}"<br>— ${author}${profile && `<br><span class="quote-profile">${profile}</span>`}</blockquote>`;
      })
      .catch(error => {
        console.error('API 호출 오류:', error);
        quoteElement.innerHTML = '<blockquote class="prompt-tip">감자에 싹이 나서 잎이 나면 묵찌바가 가능하다.<br>— Nine</blockquote>';
      });
  }

  displayRandomQuote();

  reloadButton.addEventListener('click', displayRandomQuote);
</script>
