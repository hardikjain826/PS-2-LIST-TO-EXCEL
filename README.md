// GO to problem bank - http://psd.bits-pilani.ac.in/Student/ViewActiveStationProblemBankData.aspx
// execute this code in browser console 
// developed by - Hardik Jain

const Industry_domain = 'IT' ;
// this can be Chemical , Electronics ,Finance and Mgmt , Mechanical
// change this to whatever you need

const list = document.querySelectorAll("#prohid");
const it_list_final = [];
for (let index = 0; index < list.length; index++) {
    if(list[index].querySelector("#Industry").innerText === Industry_domain ){
        it_list_final.push(list[index]);
    }
}
let data = it_list_final.map(tr => {
    let companyid = tr.querySelector('td#viewpro').getAttribute('companyid');
    let stationid = tr.querySelector('td#viewpro').getAttribute('stationid');
    let location = tr.querySelector('td#lOCATION').innerText;
    let stipend = tr.querySelector('td#stipend').innerText;
    let stationname = tr.querySelector('td#stationname').innerText;
    let link = `http://psd.bits-pilani.ac.in/Student/StationproblemBankDetails.aspx?CompanyId=${companyid}&StationId=${stationid}&BatchIdFor=13&PSTypeFor=2`;

    // return data as an array that will form one row in CSV
      return [
        `"${stationname.replace(/"/g, '""')}"`,
        `"${Industry_domain}"`,
        `"${stipend}"`,
        `"${location.replace(/"/g, '""')}"`,
        `"${link}"`
    ];

});

// convert 2D array to CSV string
let csvContent = "data:text/csv;charset=utf-8," + data.map(e => e.join(",")).join("\n");

// create a blob link to the data
let encodedUri = encodeURI(csvContent);
let link = document.createElement("a");
link.setAttribute("href", encodedUri);
link.setAttribute("download", "my_data.csv");
document.body.appendChild(link); // required for firefox

link.click(); 
