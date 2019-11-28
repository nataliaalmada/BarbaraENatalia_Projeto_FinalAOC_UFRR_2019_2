LIBRARY ieee;
USE ieee.std_logic_1164.ALL;
USE ieee.numeric_std.ALL;

ENTITY RAM IS
	port(entradaDATA : IN std_logic_vector(7 DOWNTO 0);
		  saidaDATA   : OUT std_logic_vector(7 DOWNTO 0);
		  endereco     : IN std_logic_vector(7 DOWNTO 0);
		  writememory, readmemory, clk   : IN STD_LOGIC);
END RAM;

ARCHITECTURE test OF RAM IS
	TYPE memory1 IS ARRAY(0 TO 1) OF std_logic_vector(7 DOWNTO 0);
	SIGNAL memoria : memory1:= (others => "00000000");
BEGIN
	process(Clk)
		begin
			if(rising_edge(Clk)) then
				if(writememory = '1') then
					memoria(to_integer(unsigned(endereco))) <= entradaDATA;
				end if;
				if (readmemory = '1') then
					saidaDATA <= memoria(to_integer(unsigned(endereco)));
				end if;
			end if;
	end process;
END test;
