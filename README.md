# corn-harvest
import math
import json

class CornHarvest:
    def __init__(self, file_name="corn_harvest.json"):
        self.file_name = file_name
        self.load_data()

    def load_data(self):
        """Load harvest data from a file or create a new one."""
        try:
            with open(self.file_name, "r", encoding="utf-8") as file:
                self.harvest_data = json.load(file)
        except (FileNotFoundError, json.JSONDecodeError):
            self.harvest_data = []

    def save_data(self):
        """Save harvest data to a file."""
        with open(self.file_name, "w", encoding="utf-8") as file:
            json.dump(self.harvest_data, file, indent=4, ensure_ascii=False)

    def record_harvest(self, field_name, area, yield_per_hectare):
        """Record a new corn harvest entry."""
        total_yield = area * yield_per_hectare
        entry = {
            "field_name": field_name,
            "area_hectares": area,
            "yield_per_hectare": yield_per_hectare,
            "total_yield": total_yield
        }
        self.harvest_data.append(entry)
        self.save_data()
        print(f"🌽 Recorded {total_yield} tons of corn from {field_name}.")

    def list_harvests(self):
        """List all recorded harvests."""
        if not self.harvest_data:
            print("No harvest data available.")
            return
        for harvest in self.harvest_data:
            print(f"Field: {harvest['field_name']}, Area: {harvest['area_hectares']} ha, "
                  f"Yield: {harvest['yield_per_hectare']} t/ha, Total: {harvest['total_yield']} tons")

# Example usage
def main():
    corn_harvest = CornHarvest()
    while True:
        print("\n🌽 Corn Harvest Management")
        print("1. Record Harvest")
        print("2. List Harvests")
        print("3. Exit")
        choice = input("Select an option: ")
        
        if choice == "1":
            field_name = input("Enter field name: ")
            area = float(input("Enter field area (hectares): "))
            yield_per_hectare = float(input("Enter yield per hectare (t/ha): "))
            corn_harvest.record_harvest(field_name, area, yield_per_hectare)
        elif choice == "2":
            corn_harvest.list_harvests()
        elif choice == "3":
            break
        else:
            print("Invalid choice. Try again.")

if __name__ == "__main__":
    main()
oipmkol.
