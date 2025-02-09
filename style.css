// Initialize Google Map
function initMap() {
    let map = new google.maps.Map(document.getElementById("map"), {
        zoom: 3,
        center: { lat: 20, lng: 0 },
        disableDefaultUI: true,
        styles: [
            { elementType: "geometry", stylers: [{ color: "#212121" }] },
            { elementType: "labels.text.stroke", stylers: [{ color: "#212121" }] },
            { elementType: "labels.text.fill", stylers: [{ color: "#f8b400" }] },
            { featureType: "road", stylers: [{ visibility: "off" }] },
        ],
    });

    window.map = map;
}

// Track phone number
async function trackNumber() {
    let phoneNumber = document.getElementById("phoneInput").value;
    let resultDiv = document.getElementById("result");

    if (!phoneNumber) {
        resultDiv.innerHTML = "<p style='color:red;'>Please enter a valid phone number.</p>";
        return;
    }

    try {
        let response = await fetch(`https://api.apilayer.com/number_verification/validate?number=${phoneNumber}`, {
            headers: { "apikey": "YOUR_API_LAYER_KEY" }
        });

        let data = await response.json();
        
        if (data.valid) {
            resultDiv.innerHTML = `
                <p><strong>Country:</strong> ${data.country_name}</p>
                <p><strong>Location:</strong> ${data.location || 'N/A'}</p>
                <p><strong>Carrier:</strong> ${data.carrier}</p>
            `;

            if (data.location) {
                updateMap(data.location);
            }
        } else {
            resultDiv.innerHTML = "<p style='color:red;'>Invalid phone number.</p>";
        }
    } catch (error) {
        resultDiv.innerHTML = "<p style='color:red;'>Error fetching data.</p>";
    }
}

// Update Google Map with the new location
function updateMap(location) {
    let geocoder = new google.maps.Geocoder();
    geocoder.geocode({ address: location }, function(results, status) {
        if (status === "OK") {
            let map = window.map;
            map.setCenter(results[0].geometry.location);
            map.setZoom(10);

            new google.maps.Marker({
                map: map,
                position: results[0].geometry.location,
                animation: google.maps.Animation.DROP
            });
        }
    });
}

// Load map on window load
window.onload = initMap;
