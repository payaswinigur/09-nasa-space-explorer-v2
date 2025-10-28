const getImageBtn = document.getElementById("getImageBtn");
const gallery = document.getElementById("gallery");

// JSON URL
const JSON_URL = "https://cdn.jsdelivr.net/gh/GCA-Classroom/apod/data.json";

getImageBtn.addEventListener("click", fetchSpaceImages);

async function fetchSpaceImages() {
  try {
    const response = await fetch(JSON_URL);
    const data = await response.json();

    gallery.innerHTML = "";

    // Shuffle array and pick 6 random entries
    const shuffled = data.sort(() => 0.5 - Math.random());
    const entries = shuffled.slice(0, 6);

    entries.forEach(item => {
      const galleryItem = document.createElement("div");
      galleryItem.className = "gallery-item";

      let description = item.explanation;
      let shortDesc = description.length > 150 ? description.slice(0, 150) + "..." : description;

      if (item.media_type === "image") {
        galleryItem.innerHTML = `
          <img src="${item.url}" alt="${item.title}" />
          <h3>${item.title}</h3>
          <p>${item.date}</p>
          <p class="desc">${shortDesc} ${description.length > 150 ? '<span class="read-more">Read more</span>' : ''}</p>
        `;
      } else if (item.media_type === "video") {
        galleryItem.innerHTML = `
          <div class="video-wrapper">
            <iframe src="${item.url}" frameborder="0" allowfullscreen></iframe>
          </div>
          <h3>${item.title}</h3>
          <p>${item.date}</p>
          <p class="desc">${shortDesc} ${description.length > 150 ? '<span class="read-more">Read more</span>' : ''}</p>
          <p><a href="${item.url}" target="_blank">Watch Video in New Tab</a></p>
        `;
      }

      gallery.appendChild(galleryItem);
    });

    // Add Read More toggle functionality
    document.querySelectorAll(".read-more").forEach(btn => {
      btn.addEventListener("click", function() {
        const desc = this.parentElement;
        desc.textContent = entries.find(e => e.title === desc.previousElementSibling.previousElementSibling.textContent).explanation;
      });
    });

  } catch (error) {
    console.error("Error fetching NASA JSON:", error);
    gallery.innerHTML = `<p>Failed to fetch data. Please try again later.</p>`;
  }
}
