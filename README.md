# ValidateTeamData
package teamplayer.teamplayer;


import java.io.FileReader;
import java.io.IOException;

import org.json.JSONArray;
import org.json.JSONObject;
import org.json.simple.parser.JSONParser;
import org.json.simple.parser.ParseException;
import org.junit.Assert;

public class testingteam {

public static void main(String[] args) throws IOException, ParseException {
		
		JSONParser jsonparse = new JSONParser();
		FileReader file =new FileReader("C:\\Users\\BOB\\eclipse-workspace\\teamplayer\\src\\main\\java\\data\\data.json");
		Object obj = jsonparse.parse(file);
		validateforigen(obj.toString());
		validatewicketkeeper(obj.toString());

		
	}

public static void validateforigen(String json) {
	
	JSONObject object = new JSONObject(json);
	JSONArray array=object.getJSONArray("player");
	int count= 0;
	for(int i=0;i<=array.length()-1;i++) {
		JSONObject Object = array.getJSONObject(i);
		String counrty = Object.getString("country");
		
		if(!counrty.equals("India")) {
			System.out.println("\n Name = "+Object.getString("name"));
			System.out.println("counrty = "+counrty);
			System.out.println("Role = "+Object.getString("role"));
			System.out.println("Price-in-crores = "+Object.getString("price-in-crores"));
			count++;
		}
	}
	
	if(count==4) {
		System.out.println("\n team has only 4 foreign players");
	}
	else {
		Assert.fail();
	}
	
}
public static void validatewicketkeeper(String json) {
	
	JSONObject object = new JSONObject(json);
	JSONArray array=object.getJSONArray("player");

	for(int i=0;i<=array.length()-1;i++) {
		JSONObject Object = array.getJSONObject(i);
		String role = Object.getString("role");
		
		if(role.equals("Wicket-keeper") || role.equals("All-Rounder")) {
			System.out.println("\n Name = "+Object.getString("name"));
			System.out.println("Country = "+Object.getString("country"));
			System.out.println(" Role = "+role);
			System.out.println("Price-in-crores = "+Object.getString("price-in-crores"));
			
		}
	}
}
}
